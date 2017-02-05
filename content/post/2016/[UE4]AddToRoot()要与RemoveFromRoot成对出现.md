---
title: "[UE4]AddToRoot()要与RemoveFromRoot成对出现"
date: "2016-10-19T15:33:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
- Error
---

如果对某个UObject执行了`AddToRoot()`，那么需要在该UObject所属的上级UOject销毁前，执行`RemoveFromRoot()`，否则当程序退出时，会出现崩溃，崩溃堆栈：

    Assertion failed: !IsRooted() [File:d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\coreuobject\public\uobject\UObjectBaseUtility.h] [Line: 135] 
     
     UE4Editor_Core!FDebug::AssertFailed() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\misc\outputdevice.cpp:421]
     UE4Editor_UnrealEd!<lambda_26419e543909ee92ebfb672b1e9c08dc>::operator()() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\unrealed\private\playlevel.cpp:384]
     UE4Editor_CoreUObject!ForEachObjectWithOuter() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\coreuobject\private\uobject\uobjecthash.cpp:678]
     UE4Editor_UnrealEd!UEditorEngine::EndPlayMap() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\unrealed\private\playlevel.cpp:380]
     UE4Editor_UnrealEd!UEditorEngine::Tick() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\unrealed\private\editorengine.cpp:1653]
     UE4Editor_UnrealEd!UUnrealEdEngine::Tick() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\unrealed\private\unrealedengine.cpp:371]
     UE4Editor!FEngineLoop::Tick() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\launchengineloop.cpp:2834]
     UE4Editor!GuardedMain() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\launch.cpp:156]
     UE4Editor!GuardedMainWrapper() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:126]
     UE4Editor!WinMain() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:202]
     UE4Editor!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:264]
     kernel32
     ntdll
