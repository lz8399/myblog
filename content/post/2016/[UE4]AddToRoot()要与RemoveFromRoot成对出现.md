+++
title= "[UE4]AddToRoot()要与RemoveFromRoot成对出现"
date= "2016-10-19T15:33:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "API", "Error", "GC"]
+++

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

{{< alert danger >}}
执行`RemoveFromRoot()`不要放在Actor自己对象的`Actor::BeginDestroy()`函数内（override 父类`BeginDestroy()`函数），即使是在`Super::BeginDestroy()`执行之前。否则退出游戏时（包括PIE模式（编辑器内运行游戏）下退出游戏）会导致崩溃。
{{< /alert >}}

override 父类`BeginDestroy()`函数并在其内部执行`RemoveFromRoot()`导致的崩溃堆栈：

    [Inline Frame] UE4Editor-Engine.dll!UObjectBaseUtility::MarkPendingKill() Line 150	C++
 	[Inline Frame] UE4Editor-Engine.dll!UWorld::MarkObjectsPendingKill::__l2::<lambda_def76fd07ced75fbbe91915eb5003628>::operator()(UObject * Object) Line 1500	C++
 	[Inline Frame] UE4Editor-Engine.dll!Invoke(UWorld::MarkObjectsPendingKill::__l2::<lambda_def76fd07ced75fbbe91915eb5003628> &) Line 45	C++
 	UE4Editor-Engine.dll!UE4Function_Private::TFunctionRefCaller<<lambda_def76fd07ced75fbbe91915eb5003628>,void __cdecl(UObject * __ptr64)>::Call(void * Obj, UObject * & <Params_0>) Line 251	C++
 	[Inline Frame] UE4Editor-CoreUObject.dll!UE4Function_Private::TFunctionRefBase<TFunctionRef<void __cdecl(UObject *)>,void __cdecl(UObject *)>::operator()(UObject * <Params_0>) Line 290	C++
 	UE4Editor-CoreUObject.dll!ForEachObjectWithOuter(const UObjectBase * Outer, TFunctionRef<void __cdecl(UObject *)> Operation, bool bIncludeNestedObjects, EObjectFlags ExclusionFlags, EInternalObjectFlags ExclusionInternalFlags) Line 711	C++
 	UE4Editor-Engine.dll!UWorld::MarkObjectsPendingKill() Line 1503	C++
 	UE4Editor-UnrealEd.dll!UEditorEngine::EndPlayMap() Line 415	C++
 	UE4Editor-UnrealEd.dll!UEditorEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 1957	C++
 	UE4Editor-UnrealEd.dll!UUnrealEdEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 403	C++
 	UE4Editor.exe!FEngineLoop::Tick() Line 3495	C++
 	[Inline Frame] UE4Editor.exe!EngineTick() Line 62	C++
 	UE4Editor.exe!GuardedMain(const wchar_t * CmdLine, HINSTANCE__ * hInInstance, HINSTANCE__ * hPrevInstance, int nCmdShow) Line 166	C++
 	UE4Editor.exe!WinMain(HINSTANCE__ * hInInstance, HINSTANCE__ * hPrevInstance, char * __formal, int nCmdShow) Line 209	C++

崩溃的函数位置：

    FORCEINLINE void MarkPendingKill()
	{
		check(!IsRooted());
		GUObjectArray.IndexToObject(InternalIndex)->SetPendingKill();
	}

    
{{< alert success >}}
建议重写`AActor::EndPlay()`并在其内部执行`RemoveFromRoot`。这样即使在PIE模式下退出游戏或者Game模式退出游戏都不会崩溃
{{< /alert >}}
    
    void AActor::EndPlay(const EEndPlayReason::Type EndPlayReason)
    