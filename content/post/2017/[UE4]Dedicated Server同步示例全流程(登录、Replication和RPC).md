+++
title= "[UE4]Dedicated Server同步示例全流程(登录、Replication和RPC)"
date= "2017-02-25T20:33:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

转载请注明原文出处：https://dawnarc.com

keywords：UE4、Replication、Relicate、reliable、RPC、RTS Movement、Dedicated Server、属性同步、位移同步、专用服务器、demo、example

实例的完整工程下载地址见文章底部

##### 属性同步
步骤：  
1，对属性添加UPROPERTY(Replicated)宏：

    //Player display name
	UPROPERTY(Replicated)
		FString Alias_;

2，属性所在的class中重写函数GetLifetimeReplicatedProps：  
需要头文件：

    #include "Net/UnrealNetwork.h"
    
重写函数：

    void AReplTestCharacter::GetLifetimeReplicatedProps(TArray< FLifetimeProperty > & OutLifetimeProps) const
    {
        Super::GetLifetimeReplicatedProps(OutLifetimeProps);

        DOREPLIFETIME(AReplTestCharacter, Alias_);
    }
    
##### RPC（远程执行调用）
步骤：  
1，对需要远程执行的函数添加宏UFUNCTION(Server, Reliable, WithValidation)或者UFUNCTION(Client, Reliable)。其中Server表示在客户端调用，在服务端执行；WithValidation表示是否需要验证函数，加上的画需要添加函数：bool MyFun_Validate()，函数提内容写在MyFun_Implementation函数内。cpp中不需要与函数名同名的函数体，只需要实现_Validate和_Implementation两个函数即可。
头文件：

    //移动角色(只在服务端执行的函数)
	UFUNCTION(Server, Reliable, WithValidation)
		void ServerMoveToDest(APawn* Panw, const FVector DestLocation);
	bool ServerMoveToDest_Validate(APawn* Panw, const FVector DestLocation);
	void ServerMoveToDest_Implementation(APawn* Panw, const FVector DestLocation);
    
CPP：

    bool AReplTestPlayerController::ServerMoveToDest_Validate(APawn* Panw, const FVector DestLocation)
    {
        return true;
    }

    void AReplTestPlayerController::ServerMoveToDest_Implementation(APawn* Pawn, const FVector DestLocation)
    {
        //logic...
    }
    
**三种 RPC 函数区别**：

+ UFUNCTION(Server, Reliable, WithValidation) 客户端请求，服务端执行。  
使用场景：涉及到数据安全的行为，比如：砍一刀扣血，扣血条件判定以及血量修改，都应该放在服务端执行。
+ UFUNCTION(Client, Reliable) 服务端请求，客户端执行，{{< hl-text red >}}也可能是服务端执行{{< /hl-text >}}。  
使用场景：只是表现相关，不涉及数据修改的行为，比如：装备升级，整备的属性修改发生在服务端，升级成功后的外观变化，服务端需要通知客户端替换武器 Mesh 和材质。
+ UFUNCTION(NetMulticast, Reliable) 服务端先执行，然后所有连接的客户端再执行。  
使用场景：当前客户端做的表现也希望其他客户端也看到，比如：播放攻击动作，客户端A控制的角色A播放攻击动作，希望所有其他客户端也能看见角色A播放了攻击动作。  
NetMulticast一般可以设置为 Unreliable ，表示如果网络不通畅，不重新发送 UDP 消息，比如上述装备升级，如果网络问题导致客户端未能更新装备外观，影响也不大，Unreliable 可以节省带宽。
	
{{< alert warning >}}
UFUNCTION(Client, Unreliable) 并不表示是一定在客户端执行！！！也可能是服务端执行。官方文档：
Since the server can own actors itself, a "Run on Owning Client" event may actually run on the server, despite its name.
{{< /alert >}}

**什么时候 Client function 才会在 Client 执行？**  
{{< hl-text red >}}如果调用 Client function 的对象是在 Server (NM_DedicatedServer) 创建的，那么该对象上的 Client function 始终会在 Server 执行，且 Client (NM_Client) 不会触发。{{< /hl-text >}}  
{{< hl-text red >}}如果是非 Server 创建的对象，比如：PlayerController ，那么其内部的 Client function 会在客户端执行。{{< /hl-text >}}  
{{< hl-text red >}}如何在 Server 上获取这个 Client 的 PlayerController : 重写 AGameMode::InitNewPlayer() 或者 AGameMode::PostLogin() ，PlayerController 会作为参数传递进来，将这个 PlayerController 指针保存下来。{{< /hl-text >}}

**NetMulticast function 没有在 Client 触发的问题**  
{{< hl-text red >}}并不是定义了 NetMulticast function ，就一定会在 Client 执行。{{< /hl-text >}}  
{{< hl-text red >}}比如，在服务端生成了一个 Actor ，且在服务端执行该 Actor 上的 Multicast function ，默认情况下该 Multicast function 只会在 Server 执行。{{< /hl-text >}}  
如果要使该 Actor 的 Multicast function 在客户端也执行，需要执行以下步骤（缺一不可。4.19开始，之前的版本不需要这样设置）：

+ 除了对该 Actor 执行 `bReplicates = true;` 外，还要执行 `bNetUseOwnerRelevancy = true;`
+ 该 Actor Spawn 之后，需要执行 `Actor->SetOwner(NewOwner);`，这个 NewOwner 是一个 Replicated 对象，比如 Character 。对应的Get接口为：`GetOwner()`。

https://docs.unrealengine.com/latest/INT/Gameplay/Networking/Blueprints/index.html 

##### 角色身上需要设置的属性
{{< figure src="/img/20170225-[UE4]RTS游戏的位移同步示例（Replication和RPC）/[UE4]RTS游戏的位移同步示例（Replication和RPC）-01.jpg">}}
角色蓝图上的这几个属性默认是勾选的。如果是C++，对应的属性名也是这几个。

登陆界面：
{{< figure src="/img/20170225-[UE4]RTS游戏的位移同步示例（Replication和RPC）/[UE4]RTS游戏的位移同步示例（Replication和RPC）-02.jpg">}}

多个客户端连上服务端的最终情景：
{{< figure src="/img/20170225-[UE4]RTS游戏的位移同步示例（Replication和RPC）/[UE4]RTS游戏的位移同步示例（Replication和RPC）-03.jpg">}}

#### 同步相关的基础概念
##### NetMode
每个Actor有个接口：AActor::GetNetMode()，返回值意思如下：

+ NM_Standalone：表示当前Actor在独立服务器（单机模式），可以执行客户端、服务端的所有功能。
+ NM_DedicatedServer：表示当前Actor在专用服务器上，只能执行服务端相关的功能。
+ NM_ListenServer：官方文档上解释的很少，我在官方论坛上问了下得到的几个解释是，<font color=red>ListenServer可以被游戏内的某个玩家的机器当作服务器，该服务器拥有操作每个客户端角色的权利。这种模式下，更方便来创建服务器；缺点是承载人数较少。</font>个人理解是ListenServer可能更适合做局域网游戏，因为这种既不需要考虑外挂也不需要考虑承载压力。
+ NM_Client：当客户端未连接 Dedicated Server 时，NetMode 为 NM_Standalone， 连接成功之后，客户端的 NetMode 就变成了 NM_Client 。

<font color=red>DedicatedServer没有客户端的相关功能，只接收远程客户端的网络请求，适合承载大规模玩家在线。</font>另外连接DedicatedServer的客户端，是没有权限直接修改其他玩家的数据，因为客户端上的大部分Object的Role枚举都是ROLE_AutonomousProxy（如果你逻辑有bug，也是可以被客户端发送非法请求串改其他角色的数据，所以这里所说的没有权限修改，不要以为DedicatedServer可以帮你反外挂），但是在ListenServer的玩家主机上可以，因为他拥有其他所有玩家的实例（Role枚都是ROLE_Authority类型）。UE4的一些API内部有权限检测的逻辑：判断当前Role类型是否为ROLE_Authority，这样避免非法修改数据。

##### Role
每个Actor有个公开属性：AActor::Role。表示当前Actor的作用权限，枚举值有：

+ ROLE_SimulatedProxy：表示当前Actor是一个模拟服务端的Actor状态Object，无法修改服务端上的数据，也没有权限执行远程函数（Reliable标识的UFUNCTION）。DedicatedServer服务器中创建的对象，都是ROLE_Authority，这些对象映射在客户端上的对象则都是ROLE_SimulatedProxy。
+ ROLE_AutonomousProxy：与ROLE_SimulatedProxy相似，区别是ROLE_AutonomousProxy有权限执行远程函数，但是远程函数必须是该Object身上的，其他Object上的远程函数没有权限执行。
+ ROLE_Authority：最高权限，即可以修改Server上的属性，又可以执行任何Objecct身上的远程函数。Standalone服务器中，所有对象都是ROLE_Authority。

##### NetMode 和 Role 关系概述

+ 当 NetMode 为 NM_Standalone 或者 NM_DedicatedServer 时，所有对象的 Role 都为 ROLE_Authority 。
+ 当 NetMode 为 NM_Client 时，服务端 Spawn 出来的所有 Character 对象，在每个客户端的 Role 都为 ROLE_SimulatedProxy；当前客户端 PlayerController 对象的 Role 为 ROLE_AutonomousProxy ，当前客户端无法获取其他客户端的PlayerController，如果使用其他客户端的 Character 执行 Character::GetController()，则返回NULL。

##### 关键函数

1，客户端登陆

    void UMyUserWidget::OnBtnLoginClick()
    {
        if (APlayerController* PC = GetWorld()->GetFirstPlayerController())
        {
            FString URL = FString::Printf(TEXT("%s:%s?Alias=%s"), *(TxtServerIP->GetText().ToString()), *(TxtServerPort->GetText().ToString()), *(TxtUsername->GetText().ToString()));
            PC->ClientTravel(*URL, TRAVEL_Absolute);
        }
    }
	
拒绝非法登陆请求（2018-08-05更新，未同步到文章末尾的demo工程）：

	void AFPSGameMode::PreLogin(const FString& Options, const FString& Address, const FUniqueNetIdRepl& UniqueId, FString& ErrorMessage)
	{
		Super::PreLogin(Options, Address, UniqueId, ErrorMessage);

		FString UserName = UGameplayStatics::ParseOption(Options, TEXT("UserName")).TrimStart().TrimEnd();
		if (UserName.Len() == 0 || UserMap.Find(UserName))
		{
			//deny client's login request.
			ErrorMessage = TEXT("User login repeatly!");
		}
	}
	
将`ErrorMessage`设置为非空字符串，就表示拒绝客户端的链接。

2，GameMode::InitNewPlayer()，处理登陆请求时的自定义参数，比如账号名和密码。

    FString AReplTestGameMode::InitNewPlayer(APlayerController* NewPlayerController, const FUniqueNetIdRepl& UniqueId, const FString& Options, const FString& Portal)
    {
        FString Rs = Super::InitNewPlayer(NewPlayerController, UniqueId, Options, Portal);
        if (AReplTestPlayerController* RTPC = Cast<AReplTestPlayerController>(NewPlayerController))
        {
            FString Alias = UGameplayStatics::ParseOption(Options, TEXT("Alias")).Trim();
            if (Alias.Len() == 0 || AliasMap.Find(Alias))
            {
                return Rs;
            }

            RTPC->SetPlayerAlias(Alias);
            
            PlayerData Data;
            Data.Alias = Alias;
            AliasMap.Add(Alias, Data);
        }

        return Rs;
    }

3，GameMode::PostLogin()，登陆完成后的回调函数，创建角色可以放在这个函数中处理。
    
    void AReplTestGameMode::PostLogin(APlayerController* NewPlayer)
    {
        Super::PostLogin(NewPlayer);

        if (GetNetMode() == NM_DedicatedServer)
        {
            PlayerCount++;
            if (CharClass)
            {
                if (AReplTestCharacter* Player = GetWorld()->SpawnActor<AReplTestCharacter>(CharClass, SpawnLoc, SpawnRot))
                {
                    PlayerList.Add(Player);

                    /*if (AMyAIController* AIC = GetWorld()->SpawnActor<AMyAIController>(SpawnLoc, SpawnRot))
                    {
                        AIC->Possess(Player);
                    }*/

                    Player->SpawnDefaultController();

                    //设置角色的显示名称
                    if (AReplTestPlayerController* RTPC = Cast<AReplTestPlayerController>(NewPlayer))
                    {
                        if (PlayerData* Data = AliasMap.Find(RTPC->PlayerAlias()))
                        {
                            Player->SetAlias(*(Data->Alias));
                            Data->RTC = Player;

                            if (AMyAIController* AIC = Cast<AMyAIController>(Player->GetController()))
                            {
                                AIC->SetPlayerAlias(Data->Alias);
                            }
                        }
                    }
                }
            }
        }
    }

    
4，Character::BeginPlay()，当创建的Character进入场景时的回调函数，绑定摄像机的逻辑可以放在这个函数中

    void AReplTestCharacter::BeginPlay()
    {
        Super::BeginPlay();
        if (ROLE_SimulatedProxy == Role && NM_Client == GetNetMode())
        {
            if (APlayerController* PC = GetWorld()->GetFirstPlayerController())
            {
                if (AReplTestPlayerController* RTPC = Cast<AReplTestPlayerController>(PC))
                {
                    //因为一个客户端首次加载时会有多个玩家的角色进入场景，这里判断哪个角色才是当前客户端的
                    if (Alias_ == RTPC->PlayerAlias())
                    {
                        PC->SetViewTarget(this);
                        RTPC->SetSimulatedCharacter(this);
                    }
                }
            }
        }
    }

    
5，客户端判断鼠标点击事件，这里加了一个保护，如果鼠标前后两次点击的坐标距离相差小于120，则不向服务端发送位移请求，防止频繁点击时发送消息太频繁。


    void AReplTestPlayerController::MoveToMouseCursor()
    {
        // Trace to see what is under the mouse cursor
        FHitResult Hit;
        GetHitResultUnderCursor(ECC_Visibility, false, Hit);

        if (Hit.bBlockingHit)
        {
            if (FVector::Dist(LastDestLoc, Hit.ImpactPoint) > 120)
            {
                LastDestLoc = Hit.ImpactPoint;
                SetNewMoveDestination(Hit.ImpactPoint);
            }
        }
    }
    
6，服务端处理Move请求的函数，ServerMoveToDest_Validate判断请求的逻辑是否合法：Pawn是不是当前客户端操控的角色，防止操控其他玩家的角色。

    bool AReplTestPlayerController::ServerMoveToDest_Validate(APawn* Pawn, const FVector DestLocation)
    {
        //判断请求是否非法，不允许当前客户端操控其他客户端的角色
        bool Rs = false;
        if (AReplTestCharacter* RTC = Cast<AReplTestCharacter>(Pawn))
        {
            Rs = RTC->Alias() == PlayerAlias();
        }
        return Rs;
    }

    void AReplTestPlayerController::ServerMoveToDest_Implementation(APawn* Pawn, const FVector DestLocation)
    {
        if (AMyAIController* AIC = Cast<AMyAIController>(Pawn->GetController()))
        {
            AIC->MoveToLocation(DestLocation);
        }
    }



##### 注意事项：  
1，Replicated属性只能在服务端修改  
Replicated属性只允许服务端修改后通知客户端，而不允许客户端修改Replicated属性后通知到服务端。
参考：Only the server can replicate variables or multicast events to all clients  
https://answers.unrealengine.com/questions/459423/change-variable-in-client-want-server-to-see-it-bu.html

2，Server或者Client函数参数只能时指针或者引用，而不能是对象  
比如如果参数是FString，那么必须是引用：const FString& Str，而不能是FString对象。

3，HUD的构造函数在服务端也会执行，但是DrawHUD()函数不会在服务端执行。
也就是说你要在HUD中判断当前程序是客户端还是服务端，可以不用考虑DrawHUD()函数。

4，当客户端登陆成功后，客户端所有的对象都会被重置，登陆前设置的对数属性值将变为默认值。  
比如在启动游戏后登陆之前，你给PlayerController上的string属性设置为"abc"，那么登陆成功后，这个属性值就变成了空字符串。

5，GameMode、AIController是为服务端设计的，PlayerController是为客户端设计的。两者虽然在客户端和服务端都可访问，但是前者是在服务端创建的，后者是在客户端创建的，比如PlayerController::GetHitResultAtScreenPosition只在客户端生效，而GameMode::PostLogin()只在服务端生效。

6，服务端的AIController::MoveToLocation()的效果相当于客户端UNavigationSystem::SimpleMoveToLocation()。AIController::MoveToLocation()内部有去调用NavigationSystem相关的接口。

7，客户端的PlayerController可以不用Possess玩家角色，因为客户端相关数据都是以服务端为准，操作角色也是在服务端完成，一般只需要对该角色绑定摄像机即可。

8，如果_Validate()函数返回false，则服务器会会认为客户端非法，并主动断开该客户端。断开客户端时服务端会打印：

    LogRep: Error: ReceivedRPC: RPC_GetLastFailedReason: XXXX_Validate
    LogNet: Error: UActorChannel::ProcessBunch: Replicator.ReceivedBunch failed.  Closing connection. RepObj: ReplTestPlayerController /Game/TopDownCPP/Maps/TopDownExampleMap.TopDownExampleMap:PersistentLevel.ReplTestPlayerController_1, Channel: 2

9，当前客户端只能获取当前控制角色的Controller，无法获取其他客户端的Controller，比如玩家A在玩家B的角色为C1，那么调用C1->GetController()时返回NULL。

10，动画同步  
角色X在客户端A播放一个攻击动作，并且角色X在客户端B的视野内，此时需要客户端B也能同步看到角色X的动画，流程如下：  
{{< hl-text primary >}}
客户端发送请求 -》 服务端执行函数（假设叫ServerPlayAnim()） -》 ServerPlayAnim函数内调用NetMulticast函数 -》 NetMulticast函数内执行播放动画的逻辑。
{{< /hl-text >}}

11，编辑器模式下，即使勾选了 `Run Dedicated Server`，默认是不会自动连接专用服务器的，如果希望游戏启动时就自动连接专用服务器，需要勾选：`Auto Connect to Server` （Project Settings -> Level Editor -> Play -> Multiplayer Options），如果你自己实现了登陆逻辑，那么就不要勾选这个。如果是为了方便测试跳过登陆，可以勾选这个选项，并实现对应逻辑。

##### 常见问题：
1. 如果出现以下错误，表示Reliable函数的参数名和引擎生成的代码有同名的情况，把参数名重新改一下即可。

    error : Function parameter: 'Pawn' cannot be defined in 'ServerMoveToDest' as it is already defined in scope 'Controller' (shadowing is not allowed)

2. 如果服务端SpawnActor时返回NULL，且参数传递都正确，可能是服务端上的对应Actor未清理，比如客户端崩掉了，导致了服务端的Actor未即时清理。

3. 执行UNavigationSystem::SimpleMoveToLocation(MyCharacter()->GetController(), Location);时位移无效（假设已经生成了NavMesh）。原因是MyCharacter是在客户端生成的，客户端PlayerController传递给NavigationSystem()时执行无效，需要在服务端Spawn这个Character，然后再给其Spawn出一个AIController并Possess。官方模版项目，传递给NavigationSystem的是PlayerController且位移有效，是因为模版项目中设置的DefautlPawnClass，其实是服务端Spawn出来的Character，执行位置也是在服务端。

4. 在打包版本下，客户端的玩家行走时，摄像机有抖动和卡顿（编辑器模式下正常），原因是没有勾选SpringArmComponent的Lag属性：Enable Camera Lag、Enable Camera Rotation Lag
{{< figure src="/img/20170225-[UE4]RTS游戏的位移同步示例（Replication和RPC）/[UE4]RTS游戏的位移同步示例（Replication和RPC）-04.jpg">}}
Dedicated Servers, Jitter, Matchmaking  
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/96598-dedicated-servers-jitter-matchmaking

5. 旋转视角时，NM_Standalone 模式下执行 `APlayerController::AddYawInput()` 或者 `APawn::AddControllerYawInput()` 没有问题，但是 NM_Client 模式下失效。  
原因：  
可能是Use Controller Rotation Yaw 设置为 false。  
解决办法：  
有些情况下，我们不希望使用 `Controller Rotation Yaw` 作为角色的朝向，那么此时想旋转角色方向，使用如下方式：

		void AMyPlayerController::Turn(float Rate)
		{
			// calculate delta for this frame from the rate information
			if (Rate != 0.f)
			{
				if (AActor* Target = GetViewTarget())
				{
					Target->AddActorLocalRotation(FRotator(0.f, Rate * InputYawScale, 0.f));
				}
			}
		}

	`UCameraComponent::AddRelativeRotation()` 也可以旋转视角，但是其旋转速率是 `AActor::AddActorLocalRotation()` 的两倍。原因不清楚。。。
	
6. 假设角色蓝图中有两个Component：A 和 B，A 设置为 `A->SetOnlyOwnerSee(true)`，且 B 附加在 A 上： `B->SetupAttachment(A)`，那么只能第一个登陆的角色正常，之后登陆的角色会消失不见。  
解决办法：  
这种情况下，A 不要 Attach B，如果要 Attach，B 设置为 `SetOnlyOwnerSee(false)`（默认为false）；或者 A 也隐藏掉。

7. 如果角色身上 Attach 了一个 BoxComponent 或者 SphereComponent，那么这个Component的 `CollisionProfileName` 不要设置为 `Projectile`（First Person Shooter模版项目中的自定义 `Collision Channel`），（能否设置为其他没试过，最好默认），如果设置成 `Projectile`，那么角色在移动时会不停抖动（Standalone是否也有这种问题没试过）。

8. DedicatedServer 模式下，`SpawnActor`生成出的 Actor，且这个Actor bReplicates 设置为true， 执行`ConditionalBeginDestroy()`时，一定时间后客户端会崩掉。  
解决办法：  
`SpawnActor`生成出的 Actor，且改 Actor 同步到远程机器，销毁时，不要用`ConditionalBeginDestroy()`，而要用`Destroy()`。Standalone 模式貌似没这种限制。  
崩溃日志：
	
		Assertion failed: Index >= 0 [File:D:\Build\++UE4+Release-4.16+Compile\Sync\Engine\Source\Runtime\CoreUObject\Public\UObject/UObjectArray.h] [Line: 455] 

		UE4Editor_Core!FDebug::AssertFailed() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\private\misc\assertionmacros.cpp:349]
		UE4Editor_Engine!UNetDriver::ServerReplicateActors_BuildConsiderList() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:2600]
		UE4Editor_Engine!UNetDriver::ServerReplicateActors() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:3159]
		UE4Editor_Engine!UNetDriver::TickFlush() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:355]
		UE4Editor_Engine!TBaseUObjectMethodDelegateInstance<0,UNetDriver,void __cdecl(float)>::ExecuteIfSafe() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\public\delegates\delegateinstancesimpl.h:858]
		UE4Editor_Engine!TBaseMulticastDelegate<void,float>::Broadcast() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\public\delegates\delegatesignatureimpl.inl:937]
		UE4Editor_Engine!UWorld::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\leveltick.cpp:1506]
		UE4Editor_UnrealEd!UEditorEngine::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\editor\unrealed\private\editorengine.cpp:1633]
		UE4Editor_UnrealEd!UUnrealEdEngine::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\editor\unrealed\private\unrealedengine.cpp:386]
		UE4Editor!FEngineLoop::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\launchengineloop.cpp:3119]
		UE4Editor!GuardedMain() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\launch.cpp:166]
		UE4Editor!GuardedMainWrapper() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:134]
		UE4Editor!WinMain() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:210]
		UE4Editor!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:253]
		kernel32
		ntdll

示例工程下载地址：  
http://pan.baidu.com/s/1o7MzmRo
    
##### 参考文章
属性同步：  
http://blog.csdn.net/yangxuan0261/article/details/54766955  
RPC：  
http://blog.csdn.net/yangxuan0261/article/details/54766951

***
`天下事，成于精而败于众，立于诚而倾于奢。`