---
title: "[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数"
date: "2017-05-15T23:31:02+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

keywords: UE4、Overlap、Hit、Event、Callback、C++、Blueprint、Box Collision、BoxComponent、SphereComponent、Trace Channel、碰撞

### BoxComponent的Overlap事件
##### 1，C++中的代码编写
这里我们演示的例子，是在角色身上创建一个BoxComponent，假设角色的C++ class叫AMyCharacter。
MyCharacter.h头文件中定义：

    //Box对象
    UBoxComponent* CollisionMesh;

    //OverlapBegin事件的回调函数，注意函数签名！
    UFUNCTION()
        void OnTestOverlapBegin(class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult);

    //OverlapEnd事件的回调函数，注意函数签名！
    UFUNCTION()
        void OnTestOverlapEnd(class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex);

{{< alert danger >}}
回调函数一定要加UFUNCTION()，否则无法注册成功，因为注册函数时使用了UE4编译器的反射。
{{< /alert >}}

MyCharacter.cpp的构造函数中：

    //创建BoxComponent
    CollisionMesh = CreateDefaultSubobject<UBoxComponent>(TEXT("TestCollision"));
    CollisionMesh->SetBoxExtent(FVector(200.f, 200.f, 96.f));
    CollisionMesh->bDynamicObstacle = true;
    CollisionMesh->SetupAttachment(GetRootComponent());
    //如果需要Overlap事件，将bGenerateOverlapEvents设置为true。如果不设置，默认也为true。
    CollisionMesh->bGenerateOverlapEvents = true;

    //注意：要触发Overlap事件，SetCollisionResponseToAllChannels要么不设置，要么设置为ECR_Overlap。
    CollisionMesh->SetCollisionResponseToAllChannels(ECR_Overlap);
    /*CollisionMesh->SetCollisionResponseToChannel(ECC_WorldStatic, ECR_Block);
    CollisionMesh->SetCollisionResponseToChannel(ECC_WorldDynamic, ECR_Block);
    CollisionMesh->SetCollisionResponseToChannel(ECC_Pawn, ECR_Block);
    CollisionMesh->SetNotifyRigidBodyCollision(true);
    CollisionMesh->SetSimulatePhysics(true);*/

    //要触发Overlap事件，碰对对象需要勾选属性：Generate Overlap Events
    FScriptDelegate DelegateBegin;
    DelegateBegin.BindUFunction(this, "OnTestOverlapBegin");
    CollisionMesh->OnComponentBeginOverlap.Add(DelegateBegin);
    FScriptDelegate DelegateEnd;
    DelegateEnd.BindUFunction(this, "OnTestOverlapEnd");
    CollisionMesh->OnComponentEndOverlap.Add(DelegateEnd);

回调函数的函数体：

    void AMyCharacter::OnTestOverlapBegin(class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex, bool bFromSweep, const FHitResult & SweepResult)
    {
        GEngine->AddOnScreenDebugMessage(-1, 2.f, FColor::Red, FString("Begin++++++++++++ ") + SweepResult.Location.ToString());
    }

    void AMyCharacter::OnTestOverlapEnd(class AActor* OtherActor, class UPrimitiveComponent* OtherComp, int32 OtherBodyIndex)
    {
        GEngine->AddOnScreenDebugMessage(-1, 2.f, FColor::Red, FString("End--------------- ") + OtherActor->GetName());
    }

##### 2，场景中的对象属性设置
想触发Overlap事件时，场景中的碰撞对象需要勾选的选项：**Generate Overlap Events**
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-01.jpg">}}

这样，当角色走到场景对象的附近，且身上的box与该物体发生碰撞时，就可以触发Overlap事件。

### BoxComponent的Hit事件
##### 1，C++中的代码编写
MyCharacter.h头文件中定义：

    //Box对象
    UBoxComponent* CollisionMesh;

    //Hit事件的回调函数，注意函数签名！
    UFUNCTION()
            void OnTestHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit);

MyCharacter.cpp的构造函数中：

    //创建BoxComponent
    CollisionMesh = CreateDefaultSubobject<UBoxComponent>(TEXT("TestCollision"));
    CollisionMesh->SetBoxExtent(FVector(200.f, 200.f, 96.f));
    CollisionMesh->bDynamicObstacle = true;
    CollisionMesh->SetupAttachment(GetRootComponent());
    //注意：如果要让CollisionMesh->OnComponentHit的回调事件触发，必须设置：CollisionMesh->BodyInstance.SetCollisionProfileName
    CollisionMesh->BodyInstance.SetCollisionProfileName("MyCollisionProfile");
    CollisionMesh->SetNotifyRigidBodyCollision(true);

    //要触发Hit事件，碰对对象需要勾选属性：Simulation Generates Hit Events
    FScriptDelegate DelegateHit;
    DelegateHit.BindUFunction(this, "OnTestHit");
    CollisionMesh->OnComponentHit.Add(DelegateHit);

注意，上面设置的ProfileName：MyCollisionProfile，是在Project Settings中设置的，具体步骤见下文 **Collision Channel 设置**。

回调函数的函数体：

    void AMyCharacter::OnTestHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent* OtherComponent, FVector NormalImpulse, const FHitResult& Hit)
    {
        GEngine->AddOnScreenDebugMessage(-1, 2.f, FColor::Red, FString("Hit&&&&&&&&&&&&&&&& ") + Hit.Location.ToString());
    }

##### 3，场景中的碰撞对象需要设置的选项
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-09.jpg">}}
注意，当首次勾选Simulate Physics时，Collision Presets会自动修改为PhysicsActor。

* `Simulate Physics`：如果要触发Hit事件，这个属性是必须勾选的。
* `Simulation Generates Hit Events`：表示是否触发当前物体的Hit事件，如果你需要的回调事件不是这个物体的，可以不勾选该选项。
* `Collision Presets`：同上，如果不关心当前物体的碰撞规则，只是希望其他物体碰到当前物体时，能触发其他物体的碰撞事件，那么Collision Presets可以设置为默认值。

### Collision Channel 设置

打开工程设置：Edit -》 Project Settings -》 Engine -》 Collision
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-02.jpg">}}

然后点击Object Channel下的New Object Channel：
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-03.jpg">}}

写一个名字，并将Response设置为Block。
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-04.jpg">}}

然后点击Accept，这样Object Channels就多了一条记录
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-05.jpg">}}

然后点击Preset下的New：
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-06.jpg">}}

Name自己定义，这里的Name就是之前C++代码中设置ProfileName中的名字；CollisionEnabled设置为Collision Enabled；ObjectType设置为上面步骤添加的记录；因为我们这里需要的是Hit事件，不需要Overlap，所以这里的Collision Response设置为Block。
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-07.jpg">}}

其中 CollisionEnabled 类型如下：

+ No Collision 全部禁用，物体会坠入地表，且没有物理；
+ Query Only 只启用碰撞，不会坠入地表，但是没有物理；
+ Physics Only 只启用物理，但是会坠入地表；
+ Collision Enabled 同事启用碰撞和物理，既不会坠入地表，同时有物理；

点击Accept之后，就在Preset列表中多了一条记录
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-08.jpg">}}

Collision Object Channel、Collision Preset、Object Type 三者联系：

{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-10.jpg">}}

+ Project Settings 中的 Object Channel 对应蓝图中 CollisionComponent 或者 MeshComponent 中的属性 Object Type 和 Object Response；
+ Project Settings 中的 Collision Preset 对应蓝图中 CollisionComponent 或者 MeshComponent 中的属性 Collision Presets；

如果蓝图中 CollisionComponent 或者 MeshComponent 中的属性 Collision Presets 选择预设好的 Preset ，则 Object Type 等其他 Collision 相关属性不可编辑。
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-11.jpg">}}

如果选择 Collision Presets 选择 Custom ，则可以相关属性可以编辑。相关参数含义是：

+ Object Type 表示当前物体所属的 Collision Channel ，即：Collision Presets拥有者对 Object Type 物体的影响，前者 忽略、重叠或者阻挡后者；
+ Object Response 表示当前物体与其他物体所对其他 Collision Channel 物体的反应：Ingore(忽略)、Overlaop(重叠)还是Block(阻挡)。

使用示例：  
假如有三个物体A、B、C，A物体身上有个 CollisionBox，希望这个 CollisionBox 只与物体B发生 Overlap，忽略掉物体C（既不 Overlap 也不 Block ）。  
方式如下：  
新建两个 Collision Channel，分别作为物体B和物体C的 Object Type；然后再新建一个
Collision Preset，假设叫 CollisionProfileA ，并设置该 Preset 对物体B的通道 Overlap ， 对物体C的通道 Ingore ，然后将物体A的 Collision Preset 设置成 CollisionProfileA。

##### C++ 设置 Collision

    //设置自定义 Collision 配置（只能在构造函数中使用）
    GetCollisionComponent()->SetCollisionProfileName("Custom");
    
    //设置指定通道的Response
	GetCollisionComponent()->SetCollisionResponseToChannel(ECC_Pawn, ECollisionResponse::ECR_Ignore);
    
    //为自己设置自定义 Collision 通道
    GetCollisionComponent()->BodyInstance.SetObjectType(ECollisionChannel::ECC_GameTraceChannel1);
    
其中 `ECollisionChannel::ECC_GameTraceChannel1` 为 Object Channels，例如：TestCollision。  

TestCollision 对应哪一个 `ECollisionChannel`，可以在DefaultEngine.ini找到，例如：  
`+DefaultChannelResponses=(Channel=ECC_GameTraceChannel1,Name="TestCollision",DefaultResponse=ECR_Block,bTraceType=False,bStaticObject=False)`

##### SetCollisionProfileName 注意事项

{{< alert danger >}}
SetCollisionProfileName 如果要完全生效，必须在 Actor 的构造函数中执行；如果在非构造函数中执行，Collision Profile 的 CollisionEnabled 不会生效，但是Collision Response 会生效。
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-12.jpg">}}
{{< /alert >}}

如果在非构造函数中执行`SetCollisionProfileName`会导致什么样的问题？  
{{< hl-text red >}}
在非构造函数中修改 CollisionProfile ，可以修改当前物体的Collision Channel，即：当前物体对其他 Object Type物体是 Ignore、Overlap 还是 Block。 但是无法修改当前物体的 CollisionEnabled ，即：是否启用物理、是否启用碰撞等设置无法生效。
{{< /hl-text >}}

### Actor的Hit事件（两种方式）
##### 方式1：OnActorHit 代理

1. C++代码的编写  
Actor的Hit事件不需要BoxComponent，只需要注册回调即可，回调函数的签名与上面例子的函数签名一样。

		FScriptDelegate DelegateHit;
		DelegateHit.BindUFunction(this, "OnTestHit");
		this->OnActorHit.Add(DelegateHit);
2. 场景中的碰撞对象需要设置的选项  
只要默认即可，不需要设置属性。

##### 注意事项：
如果是用BoxComponent去碰撞其他物体，且想触发BoxComponent的Hit事件（通过BoxComponent.OnComponentHit.Add()注册），那么<font color=red>其他物体的Simulate Physics属性必须设置为true，且Collision Presets属性不要设置为NoCollision</font>；
如果是用Actor去碰撞其他物体，且想触发Actor的Hit事件（通过Actor.OnActorHit.Add()注册），那么<font color=red>其他物体的Simulate Physics属性设置为true或false均可，且Collision Presets属性不要设置为NoCollision</font>。

##### 方式2：重写 NotifyHit 函数

	/** 
	 * Event when this actor bumps into a blocking object, or blocks another actor that bumps into it.
	 * This could happen due to things like Character movement, using Set Location with 'sweep' enabled, or physics simulation.
	 * For events when objects overlap (e.g. walking into a trigger) see the 'Overlap' event.
	 *
	 * @note For collisions during physics simulation to generate hit events, 'Simulation Generates Hit Events' must be enabled.
	 * @note When receiving a hit from another object's movement (bSelfMoved is false), the directions of 'Hit.Normal' and 'Hit.ImpactNormal'
	 * will be adjusted to indicate force from the other object against this object.
	 */
	virtual void AActor::NotifyHit(class UPrimitiveComponent* MyComp, AActor* Other, class UPrimitiveComponent* OtherComp, bool bSelfMoved, FVector HitLocation, FVector HitNormal, FVector NormalImpulse, const FHitResult& Hit);

### Actor的Overlap事件（两种方式）

##### 方式1：OnActorBeginOverlap 注册回调

1. 注册回调

		void AMyCharacter::BeginPlay()
		{
			Super::BeginPlay();

			FScriptDelegate Del;
			Del.BindUFunction(this, TEXT("OnOverlap"));
			OnActorBeginOverlap.Add(Del);
		}
		
2. 编写回调函数
	
	header
	
		UFUNCTION()
		void OnOverlap(AActor* OverlappedActor, AActor* OtherActor);
		
	cpp
		
		void ATestTD2Character::OnOverlap(AActor* OverlappedActor, AActor* OtherActor)
		{
			GEngine->AddOnScreenDebugMessage(-1, 5.f, FColor::Red, FString::Printf(TEXT("%s  %s  %s"), *GetName(), *OverlappedActor->GetName(), *OtherActor->GetName()));
		}

##### 方式2：重写 NotifyActorBeginOverlap 函数
	
	/** 
	 *	Event when this actor overlaps another actor, for example a player walking into a trigger.
	 *	For events when objects have a blocking collision, for example a player hitting a wall, see 'Hit' events.
	 *	@note Components on both this and the other Actor must have bGenerateOverlapEvents set to true to generate overlap events.
	 */
	virtual void AActor::NotifyActorBeginOverlap(AActor* OtherActor);
	
{{< alert warning >}}
注意：要启用Overlap事件，必须将目标对象的相应`Object Responses`类型设置为`Overlap`
{{< figure src="/img/20170515-[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数/[UE4]C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数-13.jpg">}}
{{< /alert >}}
	
##### Overlap事件开关

	void UPrimitiveComponent::SetGenerateOverlapEvents(bool bInGenerateOverlapEvents)

### 其他与碰撞相关：

Component自身提供的检测函数有：

    UPrimitiveComponent::LineTraceComponent();
    UPrimitiveComponent::SweepComponent();
    UPrimitiveComponent::ComponentOverlapComponent();
    UPrimitiveComponent::OverlapComponent(); 

	
C++ AActor::OnActorBeginOverlap 对应的蓝图节点为：

    EventActorBeginOverlap
	
C++ AActor::NotifyHit() 对应的蓝图节点为：

    EventHit
	

更多参考：
https://docs.unrealengine.com/latest/INT/Engine/Blueprints/UserGuide/Events/index.html#eventhit

提醒：<font color=red>4.12的碰撞有bug，会导致Hit事件不触发，建议用最新版本</font>。

***
`几个朋友祝我安乐，几个仇敌祝我灭亡。我却总是既不安乐，也不灭亡。不上不下地生活下来，都不能副任何一面的期望。──鲁迅`