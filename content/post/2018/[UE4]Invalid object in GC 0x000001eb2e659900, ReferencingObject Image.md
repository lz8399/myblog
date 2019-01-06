+++
title= "[UE4]Invalid object in GC: 0x000001eb2e659900, ReferencingObject: Image"
date= "2018-12-19T21:46:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "GC", "LoadObject", "Memory"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-008.jpg"
+++

Runtime\CoreUObject\Private\UObject\GarbageCollection.cpp
<!--more-->

Exception Throw:

    Fatal error: [File:D:\Build\++UE4\Sync\Engine\Source\Runtime\CoreUObject\Private\UObject\GarbageCollection.cpp] [Line: 623] Invalid object in GC: 0x000001eb2e659900, ReferencingObject: Image /Engine/Transient.GameEngine_0:TDGameInstance_0.CombatMainUIBP_C_0.WidgetTree_0.MiniMapUIBP_1216.WidgetTree_0.Image_0, ReferencingObjectClass: Class /Script/UMG.Image, Property Name: ResourceObject, Offset: 480, TokenIndex: 11

    UE4Editor_Core!FDebug::AssertFailed() [d:\build\++ue4\sync\engine\source\runtime\core\private\misc\assertionmacros.cpp:425]
    UE4Editor_CoreUObject!TFastReferenceCollector<1,FGCReferenceProcessor<1>,FGCCollector<1>,FGCArrayPool,0>::ProcessObjectArray() [d:\build\++ue4\sync\engine\source\runtime\coreuobject\public\uobject\fastreferencecollector.h:697]
    UE4Editor_CoreUObject!TFastReferenceCollector<1,FGCReferenceProcessor<1>,FGCCollector<1>,FGCArrayPool,0>::FCollectorTaskQueue::DoTask() [d:\build\++ue4\sync\engine\source\runtime\coreuobject\public\uobject\fastreferencecollector.h:378]
    UE4Editor_CoreUObject!TGraphTask<TFastReferenceCollector<1,FGCReferenceProcessor<1>,FGCCollector<1>,FGCArrayPool,0>::FCollectorTaskProcessorTask>::ExecuteTask() [d:\build\++ue4\sync\engine\source\runtime\core\public\async\taskgraphinterfaces.h:829]
    UE4Editor_Core!FTaskThreadAnyThread::ProcessTasks() [d:\build\++ue4\sync\engine\source\runtime\core\private\async\taskgraph.cpp:936]
    UE4Editor_Core!FTaskThreadAnyThread::ProcessTasksUntilQuit() [d:\build\++ue4\sync\engine\source\runtime\core\private\async\taskgraph.cpp:801]
    UE4Editor_Core!FTaskThreadBase::Run() [d:\build\++ue4\sync\engine\source\runtime\core\private\async\taskgraph.cpp:516]
    UE4Editor_Core!FRunnableThreadWin::Run() [d:\build\++ue4\sync\engine\source\runtime\core\private\windows\windowsrunnablethread.cpp:76]
    
Reason:  
Some assets object in memory not persisted

Solution:  
Use `UPROPERTY()` or `AddToRoot()` to persist assets in memory.
