+++
title= "[UE4]创建自定义PlayerController的方法(C++)"
date= "2016-06-02T18:15:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

例子：

    FActorSpawnParameters SpawnInfo;
    SpawnInfo.Instigator = Instigator;	
    SpawnInfo.ObjectFlags |= RF_Transient;	// We never want to save player controllers into a map
    SpawnInfo.bDeferConstruction = true;
    AMyPlayerController* NewPC = GetWorld()->SpawnActor<AMyPlayerController>(AMyPlayerController::StaticClass(), SpawnLocation, SpawnRotation, SpawnInfo);

参考自AGameMode::SpawnPlayerController()函数：

    APlayerController* AGameMode::SpawnPlayerController(ENetRole RemoteRole, FVector const& SpawnLocation, FRotator const& SpawnRotation)
    {
        FActorSpawnParameters SpawnInfo;
        SpawnInfo.Instigator = Instigator;	
        SpawnInfo.ObjectFlags |= RF_Transient;	// We never want to save player controllers into a map
        SpawnInfo.bDeferConstruction = true;
        APlayerController* NewPC = GetWorld()->SpawnActor<APlayerController>(PlayerControllerClass, SpawnLocation, SpawnRotation, SpawnInfo);
        if (NewPC)
        {
            if (RemoteRole == ROLE_SimulatedProxy)
            {
                // This is a local player because it has no authority/autonomous remote role
                NewPC->SetAsLocalPlayerController();
            }
            
            UGameplayStatics::FinishSpawningActor(NewPC, FTransform(SpawnRotation, SpawnLocation));
        }

        return NewPC;
    }