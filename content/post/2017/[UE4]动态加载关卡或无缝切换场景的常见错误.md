+++
title= "[UE4]动态加载关卡或无缝切换场景的常见错误"
date= "2017-12-22T16:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Seamless Scene"]
+++

错误：LogGameMode: Warning: CanServerTravel: Seamless travel currently NOT supported in single process PIE.  
原因：单进程PIE模式下不支持无缝切图。  
解决办法：开启两个UE4Editor，一个当服务器，一个当客户端？（未验证）  

Seamless Travel with Play in Editor  
https://answers.unrealengine.com/questions/335050/seamless-travel-with-play-in-editor.html


错误2：LogWorld: Warning: SetActiveLevelCollection attempted to use an out of date NetDriver: GameNetDriver  
原因：没有开启Steamless。  
解决办法：GameMode需要开启Seamless，即 UseSeamlessTravel = true;


错误3：

	0x00000000F6601F28 KERNELBASE.dll!UnknownFunction []
	0x00000000E84D76D4 UE4Editor-ApplicationCore.dll!FWindowsErrorOutputDevice::Serialize() [c:\unrealengine-4.18.2-release\engine\source\runtime\applicationcore\private\windows\windowserroroutputdevice.cpp:65]
	0x00000000CF8835AB UE4Editor-Core.dll!FOutputDevice::Logf__VA() [c:\unrealengine-4.18.2-release\engine\source\runtime\core\private\misc\outputdevice.cpp:70]
	0x00000000CF816259 UE4Editor-Core.dll!FDebug::AssertFailed() [c:\unrealengine-4.18.2-release\engine\source\runtime\core\private\misc\assertionmacros.cpp:414]
	0x00000000CD8D9334 UE4Editor-Engine.dll!UEngine::TickWorldTravel() [c:\unrealengine-4.18.2-release\engine\source\runtime\engine\private\unrealengine.cpp:10109]
	0x00000000CAA76201 UE4Editor-UnrealEd.dll!UEditorEngine::Tick() [c:\unrealengine-4.18.2-release\engine\source\editor\unrealed\private\editorengine.cpp:1605]
	0x00000000CB33B856 UE4Editor-UnrealEd.dll!UUnrealEdEngine::Tick() [c:\unrealengine-4.18.2-release\engine\source\editor\unrealed\private\unrealedengine.cpp:396]
	0x00000000F4BC5A26 UE4Editor.exe!FEngineLoop::Tick() [c:\unrealengine-4.18.2-release\engine\source\runtime\launch\private\launchengineloop.cpp:3296]
	0x00000000F4BD5430 UE4Editor.exe!GuardedMain() [c:\unrealengine-4.18.2-release\engine\source\runtime\launch\private\launch.cpp:166]
	0x00000000F4BD54AA UE4Editor.exe!GuardedMainWrapper() [c:\unrealengine-4.18.2-release\engine\source\runtime\launch\private\windows\launchwindows.cpp:134]
	0x00000000F4BE2379 UE4Editor.exe!WinMain() [c:\unrealengine-4.18.2-release\engine\source\runtime\launch\private\windows\launchwindows.cpp:210]
	0x00000000F4BE3D57 UE4Editor.exe!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:253]
	0x00000000F82F8102 KERNEL32.DLL!UnknownFunction []
	0x00000000F9F3C5B4 ntdll.dll!UnknownFunction []
	0x00000000F9F3C5B4 ntdll.dll!UnknownFunction []
	
原因：客户端调用ServerTravel  
解决办法：ServerTravel不要在客户端模式下调用，可以在DedicatedServer或者Standalone调用。  

***
`江天一色无纤尘，皎皎空中孤月轮。----张若虚《春江花月夜》`