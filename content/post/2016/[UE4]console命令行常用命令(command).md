---
title: "[UE4]console命令行常用命令(command)"
date: "2016-05-27T15:30:02+08:00"
categories:
- UnrealEngine4
tags:
- console
- UE4
---

修改Camera Mode（切换摄像机视角）：
Camera [modename]
其中modename的值为：

    static const FName NAME_Fixed = FName(TEXT("Fixed"));
    static const FName NAME_ThirdPerson = FName(TEXT("ThirdPerson"));
    static const FName NAME_FreeCam = FName(TEXT("FreeCam"));
    static const FName NAME_FreeCam_Default = FName(TEXT("FreeCam_Default"));
    static const FName NAME_FirstPerson = FName(TEXT("FirstPerson"));


启用debug camera：

    ToggleDebugCamera
	
显示刚体

	Show Collision

显示帧率

	stat fps
	
显示Drawcall
	
	stat scenerendering
	
显示三角面数量

	stat Engine
	
显示单帧信息：总时长、Game耗时、Draw耗时、GPU耗时

    stat unit
    
显示当前帧的时间信息（各种Tick, GC Mark，Update Overlaps等）：

    stat game
    
设置渲染分辨率为默认大小的50%

    r.ScreenPercentage 50

记录卡顿时间（通过`t.HitchThreshold`定义卡顿时长阀值）  

    stat Hitches    //或者stat DumpHitches 记录log文件
    
程序运行时一旦某帧耗时超过`t.HitchThreshold`指定的时长，则函数堆栈就会被打印出来。例如，以下 hitchdump 显示LoadObject耗时较长，则表示是加载资源导致顿卡

       477.514ms (   4)  -  Thread_4118_0 - GameThread - STATGROUP_Threads - STATCAT_Advanced
         477.510ms (   2)  -  FrameTime - STAT_FrameTime - STATGROUP_Engine - STATCAT_Advanced
           470.844ms (   1)  -  FrameTime - STAT_FrameTime - STATGROUP_Engine - STATCAT_Advanced
             470.840ms (   1)  -  World Tick Time - STAT_WorldTickTime - STATGROUP_Game - STATCAT_Advanced
               470.758ms (   5)  -  Tick Time - STAT_TickTime - STATGROUP_Game - STATCAT_Advanced
                 470.590ms (   2)  -  TG_PrePhysics - STAT_TG_PrePhysics - STATGROUP_TickGroups - STATCAT_Advanced
                   470.585ms (   2)  -  ReleaseTickGroup Block - STAT_ReleaseTickGroup_Block - STATGROUP_TickGroups - STATCAT_Advanced
                     470.579ms (   1)  -  Game TaskGraph Tasks - STAT_TaskGraph_GameTasks - STATGROUP_Threading - STATCAT_Advanced
                       470.512ms (  20)  -  FTickFunctionTask - STATGROUP_TaskGraphTasks - STATCAT_Advanced
                         470.309ms (   1)  -  BaseGameMode/Game/Map/PVP/UEDPIE_0_PVP.PVP.PersistentLevel.BaseGameMode - STATGROUP_UObjects - STATCAT_Advanced
                           469.638ms (   3)  -  LoadObject - STAT_LoadObject - STATGROUP_Object - STATCAT_Advanced
                             377.887ms (   3)  -  Self
                             26.688ms ( 533)  -  STAT_FArchiveAsync2_WaitRead - STATGROUP_Quick - STATCAT_Advanced

{{< alert warning >}}
使用stat相关命令检测性能时，需要关闭Smooth Frame Rate来保证检测结果更精准：Project Settings -》 Engine -》 General Settings -》 Framerate -》 Smooth Frame Rate。
{{< /alert >}}
    
https://docs-origin.unrealengine.com/latest/INT/Engine/Performance/StatCommands/