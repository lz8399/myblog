+++
title= "[UE4]创建自定义AIController的方法(C++)"
date= "2017-09-13T20:09:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

之前写过如何用C++创建自定义PlayerController方式：

    FActorSpawnParameters SpawnInfo;
    SpawnInfo.Instigator = Instigator;	
    SpawnInfo.ObjectFlags |= RF_Transient;	// We never want to save player controllers into a map
    SpawnInfo.bDeferConstruction = true;
    AMyPlayerController* NewPC = GetWorld()->SpawnActor<AMyPlayerController>(AMyPlayerController::StaticClass(), SpawnLocation, SpawnRotation, SpawnInfo);

如果用同样的方式，在服务端创建AIController，会有问题，执行：

    EPathFollowingRequestResult::Type AAIController::MoveToLocation(const FVector& Dest, ...);
    
返回值是Success，但是没有任何效果。

原因：  
自己设置FActorSpawnParameters相关参数，对PlayerController可行，但是对AIController，相关参数设置不一样，导致AIController在服务端失效。


解决办法：  
两种方式
##### 方式一：AIControllerClass指定
1，先为Character指定AI Controller Class，且禁用AutoPossessPlayer。这段代码可以放在构造函数中，保证在Possess之前设置好。以下3个属性也可以在角色蓝图中指定。

    AutoPossessPlayer = EAutoReceiveInput::Type::Disabled;
	AutoPossessAI = EAutoPossessAI::PlacedInWorld;
	AIControllerClass = AMyAIController::StaticClass();
    
2，Character被Spawn出来后，再执行：

    void APawn::SpawnDefaultController();
    
如果AutoPossessAI设置为Disable，则接着执行一下Possess：
    
    void AController::Possess(APawn* InPawn);
    
    
##### 方式一：SpawnActor时使用默认FActorSpawnParameters。

     AMyAIController* PC = GetWorld()->SpawnActor<AMyAIController>(AMyAIController::StaticClass(), SpawnLoc, SpawnRot);
     
不要自己设置FActorSpawnParameters，因为AIController和PlayerController表现不一样。

***
`人生一世,草生一春,来如风雨,去似微尘。----《增广贤文》`