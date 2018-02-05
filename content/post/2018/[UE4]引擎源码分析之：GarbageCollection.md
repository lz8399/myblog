+++
title= "[UE4]引擎源码分析之：GarbageCollection"
date= "2018-02-04T15:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "GC"]
draft= true
+++


Engine\Source\Runtime\CoreUObject\Private\UObject\GarbageCollection.cpp

垃圾回收的逻辑堆栈（MainThread）：

    UE4Editor-CoreUObject.dll!CollectGarbageInternal(EObjectFlags KeepFlags, bool bPerformFullPurge) Line 1496	
    UE4Editor-CoreUObject.dll!TryCollectGarbage(EObjectFlags KeepFlags, bool bPerformFullPurge) Line 1560	
    UE4Editor-Engine.dll!UEngine::PerformGarbageCollectionAndCleanupActors() Line 1134	
    UE4Editor-Engine.dll!UEngine::ConditionalCollectGarbage() Line 1108	
    UE4Editor-Engine.dll!UWorld::Tick(ELevelTick TickType, float DeltaSeconds) Line 1612	
    UE4Editor-UnrealEd.dll!UEditorEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 1481	
    UE4Editor-UnrealEd.dll!UUnrealEdEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 401	
    UE4Editor.exe!FEngineLoop::Tick() Line 3320	
    [Inline Frame] UE4Editor.exe!EngineTick() Line 62	
