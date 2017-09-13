+++
title= "[UE4]创建自定义PlayerController的方法(C++)"
date= "2016-06-02T18:15:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

一种不推荐的写法：

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
    
推荐写法：

    AMyPlayerController* PC = GetWorld()->SpawnActor<AMyPlayerController>(SpawnLoc, SpawnRot);

因为FActorSpawnParameters的参数非常多，如果自己设置，很可能有些参数设置不不正确导致不可预期的效果。