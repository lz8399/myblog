+++
title= "[UE4]动态加载关卡或无缝切换场景的资料收集"
date= "2017-12-21T12:22:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Seamless Scene"]
+++

How to open level asynchronously, without visible after load?  
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/47363-how-to-open-level-asynchronously-without-visible-after-load

Level Streaming: Move from MainMenu to World level.  
https://answers.unrealengine.com/questions/280618/level-streaming-move-from-mainmenu-to-world-level.html

How to change Map? C++ code.  
https://answers.unrealengine.com/questions/146988/how-to-load-a-level.html

Failed to load package on client  
https://answers.unrealengine.com/questions/196214/failed-to-load-package-on-client.html

What is the difference between ServerTravel and OpenLevel?  
https://answers.unrealengine.com/questions/55477/the-difference-of-the-two-functions.html

UE4中动态创建并加载流关卡  
http://blog.csdn.net/xi_niuniu/article/details/54408188

	// 获取永久性关卡  
	UWorld* PersistentWorld = GetWorld();

	if (!PersistentWorld)
	{
		UE_LOG(LogTemp, Fatal, TEXT("UDynamicLevels::LoadTileToStreamingArray >> Invalid PersistentWorld!!!"));
		return;
	}

	UE_LOG(LogTemp, Display, TEXT("aaaaaaaaaaaaaa"));

	//new StreamingClass Instance 新流关卡实例  
	UClass* StreamingClass = ULevelStreamingKismet::StaticClass();
	ULevelStreaming* StreamingLevel = Cast<ULevelStreaming>(StaticConstructObject_Internal(StreamingClass, PersistentWorld));

	// FName PackageName = TEXT("/Game/TempUmap/Level_01") 根据项目实际情况获取并设置PackageName  
	FName PackageName(TEXT("/Game/Demo/scecn_test/scene_create_role"));
	StreamingLevel->SetWorldAssetByPackageName(PackageName);

	UE_LOG(LogTemp, Display, TEXT("bbbbb"));

	//Make New Level Visible 使流关卡可见  
	StreamingLevel->bShouldBeLoaded = true;
	StreamingLevel->bShouldBeVisible = true;
	StreamingLevel->bShouldBlockOnLoad = false;

	UE_LOG(LogTemp, Display, TEXT("cccccc"));

	//Very Important, used by LevelStreaming* to load the map 设置流关卡的包名  
	StreamingLevel->PackageNameToLoad = PackageName;
	//Add to UWorld 将流关卡添加到World中  
	PersistentWorld->StreamingLevels.Add(StreamingLevel);


Levels loaded from .umap file name during Runtime flicker constantly and Lightning never finishes rebuilding  
https://answers.unrealengine.com/questions/39875/levels-loaded-from-umap-file-name-during-runtime-f.html

Unreal4 入门（关卡动态加载）  
http://blog.sina.com.cn/s/blog_7c5fd2e90101kxig.html

Unreal Engine4 C++ 动态加载Level（关卡）  
http://blog.csdn.net/qq_20309931/article/details/52850547

！！！How do I use PrepareMapChange/CommitMapChange?  
https://answers.unrealengine.com/questions/46503/how-to-use-preparemapchangecommitmapchange.html


	void AWarSoulPlayerController::TestSwitchScene(int32 Value)
	{
		if (Value)
		{
			bool rs = GetWorld()->ServerTravel(TEXT("/Game/Demo/scene/scene_01"));
			UE_LOG(LogTemp, Display, TEXT("aaa %d"), rs ? 1 : 0);
		}
		else
		{
			bool rs = GetWorld()->ServerTravel(TEXT("/Game/Demo/scene/scene_01"));
			UE_LOG(LogTemp, Display, TEXT("bbb %d"), rs ? 1 : 0);
		}
	}

如何ServerTravel()相关的回调函数（切换场景之前、切换场景之后等）：  
Runtime\Engine\Classes\GameFramework\GameModeBase.h

	/** Returns true if allowed to server travel */
	virtual bool CanServerTravel(const FString& URL, bool bAbsolute);

	/** Handles request for server to travel to a new URL, with all players */
	virtual void ProcessServerTravel(const FString& URL, bool bAbsolute = false);

	/** 
	 * called on server during seamless level transitions to get the list of Actors that should be moved into the new level
	 * PlayerControllers, Role < ROLE_Authority Actors, and any non-Actors that are inside an Actor that is in the list
	 * (i.e. Object.Outer == Actor in the list)
	 * are all automatically moved regardless of whether they're included here
	 * only dynamic actors in the PersistentLevel may be moved (this includes all actors spawned during gameplay)
	 * this is called for both parts of the transition because actors might change while in the middle (e.g. players might join or leave the game)
	 * @see also PlayerController::GetSeamlessTravelActorList() (the function that's called on clients)
	 * @param bToTransition true if we are going from old level to transition map, false if we are going from transition map to new level
	 * @param ActorList (out) list of actors to maintain
	 */
	virtual void GetSeamlessTravelActorList(bool bToTransition, TArray<AActor*>& ActorList);

	/**
	 * Used to swap a viewport/connection's PlayerControllers when seamless traveling and the new GameMode's
	 * controller class is different than the previous
	 * includes network handling
	 * @param OldPC - the old PC that should be discarded
	 * @param NewPC - the new PC that should be used for the player
	 */
	virtual void SwapPlayerControllers(APlayerController* OldPC, APlayerController* NewPC);

	/**
	 * Handles reinitializing players that remained through a seamless level transition
	 * called from C++ for players that finished loading after the server
	 * @param C the Controller to handle
	 */
	virtual void HandleSeamlessTravelPlayer(AController*& C);

	/**
	 * Called after a seamless level transition has been completed on the *new* GameMode.
	 * Used to reinitialize players already in the game as they won't have *Login() called on them
	 */
	virtual void PostSeamlessTravel();

	/** Start the transition out of the current map. Called at start of seamless travel, or right before map change for hard travel. */
	virtual void StartToLeaveMap();


	/**
	 * Spawns a PlayerController at the specified location; split out from Login()/HandleSeamlessTravelPlayer() for easier overriding
	 *
	 * @param RemoteRole the role this controller will play remotely
	 * @param SpawnLocation location in the world to spawn
	 * @param SpawnRotation rotation to set relative to the world
	 *
	 * @return PlayerController for the player, NULL if there is any reason this player shouldn't exist or due to some error
	 */
	virtual APlayerController* SpawnPlayerController(ENetRole InRemoteRole, FVector const& SpawnLocation, FRotator const& SpawnRotation);


打包时需要设置的地图选项  
https://answers.unrealengine.com/questions/196214/failed-to-load-package-on-client.html

[4.14] ServerTravel with more than the Server doesn't work in PIE  
https://answers.unrealengine.com/questions/523891/414-servertravel-with-more-than-the-server-doesnt.html

How can I change the level for all connected clients in a multiplayer game?  
https://answers.unrealengine.com/questions/50860/bp-change-level-map-in-multiplayer.html

UE4流关卡与无缝地图切换总结  
http://blog.csdn.net/u012999985/article/details/78484511

