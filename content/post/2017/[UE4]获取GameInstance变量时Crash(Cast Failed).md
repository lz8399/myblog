+++
title= "[UE4]获取GameInstance变量时Crash(Cast Failed)"
date= "2018-01-13T00:57:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++


代码（在GameMode::BeginPlay()中调用）：

	void AReleaseGameMode::SpawnMainRole()
	{
		UE_LOG(LogTemp, Log, TEXT("SpawnMainRole 11111 "));
		if (UMyGameInstance* WSGI = Cast<UMyGameInstance>(GetWorld()->GetGameInstance()))
		{
			UE_LOG(LogTemp, Log, TEXT("SpawnMainRole 22222"));
			if (ABaseCharacter* BC = GetWorld()->SpawnActor<ABaseCharacter>(WSGI->CurrentCharacter, MainRoleSpawnLoc_, MainRoleSpawnRot_))
			{
				UE_LOG(LogTemp, Log, TEXT("SpawnMainRole 333333 "));
				BC->SpawnDefaultController();
			}
		}
	}

崩溃日志：

[2018.01.12-16.47.12:367][ 94]LogTemp: SpawnMainRole 11111
[2018.01.12-16.47.12:367][ 94]LogTemp: SpawnMainRole 22222
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: === Critical error: ===
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: 
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: Fatal error!
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: 
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: Unhandled Exception: EXCEPTION_ACCESS_VIOLATION reading address 0xffffffff
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: 
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x00000000204CA74A UE4Editor-CoreUObject.dll!UStruct::IsChildOf() [c:\unrealengine-4.18.2-release\engine\source\runtime\coreuobject\public\uobject\class.h:375]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000000AA97137 UE4Editor-TestProj-Win64-DebugGame.dll!AReleaseGameMode::SpawnMainRole() [f:\source\work\project\ue4_proj\TestProj\source\TestProj\graphics\world\releasegamemode.cpp:182]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000000AA94C5D UE4Editor-TestProj-Win64-DebugGame.dll!AReleaseGameMode::BeginPlay() [f:\source\work\project\ue4_proj\TestProj\source\TestProj\graphics\world\releasegamemode.cpp:81]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001B31C8AB UE4Editor-Engine.dll!AActor::DispatchBeginPlay() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\actor.cpp:3160]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001C517480 UE4Editor-Engine.dll!AWorldSettings::NotifyBeginPlay() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\worldsettings.cpp:187]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001BA6F4C1 UE4Editor-Engine.dll!AGameStateBase::HandleBeginPlay() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\gamestatebase.cpp:177]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001C50372E UE4Editor-Engine.dll!UWorld::BeginPlay() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\world.cpp:3505]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001C42B054 UE4Editor-Engine.dll!UEngine::LoadMap() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\unrealengine.cpp:10679]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000001C3E4648 UE4Editor-Engine.dll!UEngine::Browse() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\unrealengine.cpp:9948]
[2018.01.12-16.47.15:359][ 94]LogWindows: Error: [Callstack] 0x000000000AA8CB20 UE4Editor-TestProj-Win64-DebugGame.dll!UCreateRoleWidget::OnBtnStartClick() 

原因：在Server端访问了一个在客户端赋值过的GameInstance变量。

解决办法：赋值逻辑放在Server端。

UE4的另一个bug：  
另外，在Viewport/Simulation中正常，在Package/Standalone中Cast失败，原因如下：  
Casting to game instance always fails when packaging the game  
https://answers.unrealengine.com/questions/595245/casting-to-game-instance-always-fails-when-packagi.html