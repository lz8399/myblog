+++
title= "[UE4]FMallocTBB：：Malloc  scalable_malloc() crash"
date= "2016-05-28T21:54:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++
#

    UE4Editor_Core!rml::internal::Block::freePublicObject()
    UE4Editor_Core!rml::internal::ExtMemoryPool::initTLS()
    UE4Editor_Core!FMallocTBB::Free() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\private\hal\malloctbb.cpp:115]
    UE4Editor_Core!FMemory::Free() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\public\hal\fmemory.inl:49]
    UE4Editor_MyProject_784_Win64_DebugGame!operator delete[]() [d:\workspace\unreal_project\huaikongxin2\program\client\huaikxcli\source\huaikx\huaikx.cpp:15]
    UE4Editor_MyProject_784_Win64_DebugGame!HServices::HRecvMsg::~HRecvMsg() [d:\workspace\unreal_project\huaikongxin2\program\client\huaikxcli\source\huaikx\services\network\hrecvmsg.cpp:33]
    UE4Editor_MyProject_784_Win64_DebugGame!AHGameMode::Tick() [d:\workspace\unreal_project\huaikongxin2\program\client\huaikxcli\source\huaikx\graphics\world\hgamemode.cpp:121]
    UE4Editor_Engine!AActor::TickActor() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\actor.cpp:814]
    UE4Editor_Engine!FActorTickFunction::ExecuteTick() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\actor.cpp:111]
    UE4Editor_Engine!FTickFunctionTask::DoTask() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\ticktaskmanager.cpp:262]
    UE4Editor_Engine!TGraphTask<FTickFunctionTask>::ExecuteTask() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\public\async\taskgraphinterfaces.h:999]
    UE4Editor_Core!FNamedTaskThread::ProcessTasksNamedThread() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\private\async\taskgraph.cpp:932]
    UE4Editor_Core!FNamedTaskThread::ProcessTasksUntilQuit() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\private\async\taskgraph.cpp:679]
    UE4Editor_Core!FTaskGraphImplementation::WaitUntilTasksComplete() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\core\private\async\taskgraph.cpp:1776]
    UE4Editor_Engine!FTickTaskSequencer::ReleaseTickGroup() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\ticktaskmanager.cpp:530]
    UE4Editor_Engine!FTickTaskManager::RunTickGroup() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\ticktaskmanager.cpp:1435]
    UE4Editor_Engine!UWorld::RunTickGroup() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\leveltick.cpp:704]
    UE4Editor_Engine!UWorld::Tick() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\engine\private\leveltick.cpp:1197]
    UE4Editor_UnrealEd!UEditorEngine::Tick() [d:\build\++ue4+release-4.12+compile\sync\engine\source\editor\unrealed\private\editorengine.cpp:1349]
    UE4Editor_UnrealEd!UUnrealEdEngine::Tick() [d:\build\++ue4+release-4.12+compile\sync\engine\source\editor\unrealed\private\unrealedengine.cpp:368]
    UE4Editor!FEngineLoop::Tick() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\launch\private\launchengineloop.cpp:2774]
    UE4Editor!GuardedMain() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\launch\private\launch.cpp:148]
    UE4Editor!GuardedMainWrapper() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:126]
    UE4Editor!WinMain() [d:\build\++ue4+release-4.12+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:200]
    UE4Editor!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:264]
    kernel32
    ntdll

#

    UE4Editor-Core.dll!rml::internal::ExtMemoryPool::initTLS(void)	
    UE4Editor-Core.dll!scalable_mallo()	
    UE4Editor-Core.dll!FMallocTBB::Malloc(unsigned __int64 Size, unsigned int Alignment) Line 44	C++
    UE4Editor-HuaiKX-6959-Win64-DebugGame.dll!HServices::HRecvMsg::HRecvMsg(int type, const char * data, int len) Line 20	C++
    UE4Editor-HuaiKX-6959-Win64-DebugGame.dll!AHGameMode::PushTcpMsg(int type, const char * bytes, int size) Line 131	C++
    UE4Editor-HuaiKX-6959-Win64-DebugGame.dll!HServices::HRecvThread::Run() Line 114	C++
    UE4Editor-Core.dll!FRunnableThreadWin::Run() Line 74	C++
    UE4Editor-Core.dll!FRunnableThreadWin::GuardedRun() Line 23	C++



如果在FMallocTBB::Malloc()或者FMallocTBB::Free()函数内的出现crash，比如执行到scalable_malloc()这里时，那么可以断定你的逻辑代码有内存溢出（内存寻址错误）的问题。不用怀疑是不是UE4引擎bug，仔细调试跟踪变量指针的值是否出现了不在预期内的修改。