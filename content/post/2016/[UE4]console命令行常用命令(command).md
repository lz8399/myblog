---
title: "[UE4]console命令行常用命令(command)"
date: "2016-05-27T15:30:02+08:00"
categories:
- UnrealEngine4
tags:
- console
- UE4
---

##### Editor命令（ShowFlag）
如果想在 Editor 中查看 Actor 蓝图的 Bounds（默认只能在 Static Mesh 编辑窗口中查看），可以使用 ShowFlag 命令（在编辑器窗口中按下波浪键打开输入窗口）。

开启：

    ShowFlag.Bounds 1

关闭：
    
    ShowFlag.Bounds 0
    
凡是 Show 命令能查看的参数，ShowFlag也能查看，包括Collision等。

{{< alert success >}}
如果想在游戏运行时查看指定物体的 Bounds，那么可以先执行 ShowFlag.Bounds 1，然后再以 Simulate 模式运行游戏，然后再在场景中单击要查看的物体，然后就可以显示该物体的 Bounds 信息。
{{< /alert >}}

##### 运行时命令

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

    stat Unit
    stat UnitGraph  //附带各个参数的实时曲线图
    
显示当前帧的时间信息（各种Tick, GC Mark，Update Overlaps等）：

    stat game
    
设置渲染分辨率为默认大小的50%

    r.ScreenPercentage 50

记录卡顿时间（通过`t.HitchThreshold`定义卡顿时长阀值）  

    stat Hitches    //或者stat DumpHitches 记录log文件
    
程序运行时一旦某帧耗时超过`t.HitchThreshold`指定的时长，则函数堆栈就会被打印出来。例如，以下 hitchdump 显示LoadObject耗时较长（当前行行首的时长减去下一行行首的时长就是当前行函数的耗时），则表示是加载资源导致顿卡

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
                             
查看遮挡剔除：
                             
    r.visualizeOccludedPrimitives 1

##### 性能统计图工具 Session Frontend
用于记录某段时间内的性能分析数据。

在需要开始统计的时刻执行：

    stat startfile
    
在统计完成的时刻执行：

    stat stopfile
    
此时会在路径 `Saved/Profiling/UnrealStats` 下生成数据文件。  
然后点击：Windows -》 Developer Tools -》 Session Frontend -》点击 Profiler 选项卡 -》 点击 Load 按钮，载入前面生成的数据文件。


##### GPUProfile 与 CPUProfile

GPU性能分析  
在编辑器中运行游戏时，按下 Ctrl + Shift + 逗号 ，打开 GPUProfile 面板，显示当前帧的各类计算的耗时：PostProcess、Lighting 等。注意：是当前一帧的耗时，不是平均每帧的耗时。  
如果是 在Development 打包模式下，Ctrl + Shift + 逗号 并不会打开 GPUProfile 面板，但是在 `工程名\Saved\Logs\工程名.log` 中会有 Profiling 记录，例如：

    [2018.08.26-07.56.40:320][291]Profiling the next GPU frame
    [2018.08.26-07.56.40:406][294]LogD3D11RHI: Warning: 
    [2018.08.26-07.56.40:406][294]LogD3D11RHI: Warning: 
    [2018.08.26-07.56.40:411][295]LogRHI: Perf marker hierarchy, total GPU time 4.33ms
    [2018.08.26-07.56.40:411][295]LogRHI: Warning: Profiled range was continuous.
    [2018.08.26-07.56.40:412][295]LogRHI: 100.0% 4.33ms   FRAME 635 draws 16087 prims 18018 verts
    [2018.08.26-07.56.40:412][295]LogRHI: 97.1% 4.20ms   Scene 633 draws 15751 prims 17346 verts
    [2018.08.26-07.56.40:412][295]LogRHI:     1.1% 0.05ms   PrePass DDM_AllOpaque (Forced by DBuffer) 141 draws 5744 prims 5634 verts
    [2018.08.26-07.56.40:412][295]LogRHI:        0.3% 0.01ms   BeginRenderingPrePass 1 draws 0 prims 0 verts
    [2018.08.26-07.56.40:412][295]LogRHI:     0.5% 0.02ms   ComputeLightGrid 5 draws 5 prims 0 verts
    [2018.08.26-07.56.40:412][295]LogRHI:        0.3% 0.01ms   CullLights 30x17x32 NumLights 0 NumCaptures 1 4 draws 4 prims 0 verts
    [2018.08.26-07.56.40:412][295]LogRHI:        0.2% 0.01ms   Compact 1 draws 1 prims 0 verts
    [2018.08.26-07.56.40:412][295]LogRHI:     0.1% 0.00ms   BeginOcclusionTests 16 draws 192 prims 128 verts
    [2018.08.26-07.56.40:412][295]LogRHI:        0.1% 0.00ms   ViewOcclusionTests 0 16 draws 192 prims 128 verts
    [2018.08.26-07.56.40:412][295]LogRHI:           0.1% 0.00ms   IndividualQueries 16 draws 192 prims 128 verts

CPU性能分析  
CPU性能分析可以通过 `stat scenerendering` 、`stat game` 等命令分析，如果某类型的 draw call 数量特别高，说明这是 CPU 的瓶颈所在。

{{< alert danger >}}
如果是在编辑器模式，建议以“新窗口”(New Editor Window)PIE模式运行，如果是在编辑器的Viewport中运行，会把编辑器的消耗也算进去（即使是全屏模式）。
{{< /alert >}}

CPU Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance/CPU

GPU Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance/GPU

##### 工程设置相关
                             
{{< alert warning >}}
使用stat相关命令检测性能时，需要关闭Smooth Frame Rate来保证检测结果更精准：Project Settings -》 Engine -》 General Settings -》 Framerate -》 Smooth Frame Rate。
{{< /alert >}}

##### 运行时期间用C++执行console命名

	UKismetSystemLibrary::ExecuteConsoleCommand(UObject* WorldContextObject, 
		const FString& Command, class APlayerController* SpecificPlayer = NULL )

##### 运行时期间修改画质级别

Unreal Engine 4 Save and Load Graphics Settings using Blueprints Tutorial  
https://www.youtube.com/watch?v=5AXA2CrPwTo

Change Graphics Settings In-Game - Unreal Engine 4 Tutorial  
https://www.youtube.com/watch?v=T90vqA9x5so

Scalability Reference  
https://docs.unrealengine.com/en-us/Engine/Performance/Scalability/ScalabilityReference

{{< alert success >}}
蓝图`Execute Console Command`节点（C++接口：`UKismetSystemLibrary::ExecuteConsoleCommand()`）在 Shipping 模式下仍然有效。
{{< /alert >}}

##### 查询命令的参数值

C++ 或者 蓝图中使用查询函数

	float UKismetSystemLibrary::GetConsoleVariableFloatValue(UObject* WorldContextObject, const FString& VariableName)
	
	int32 UKismetSystemLibrary::GetConsoleVariableIntValue(UObject* WorldContextObject, const FString& VariableName)
	
例如：

先在命令行执行

	r.ScreenPercentage 200
	
然后通过蓝图或者C++查询
	
	float RetVal = KismetSystemLibrary::GetConsoleVariableIntValue(this, TEXT("r.ScreenPercentage"));
	//RetVal is 200.f

##### 官方文档

https://docs-origin.unrealengine.com/latest/INT/Engine/Performance/StatCommands/
