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

记录卡顿时间（通过t.HitchThreshold定义卡顿时长阀值）  

    stat Hitches    //或者stat DumpHitches 记录log文件

{{< alert warning >}}
使用stat相关命令检测性能时，需要关闭Smooth Frame Rate来保证检测结果更精准：Project Settings -》 Engine -》 General Settings -》 Framerate -》 Smooth Frame Rate。
{{< /alert >}}
    
https://docs-origin.unrealengine.com/latest/INT/Engine/Performance/StatCommands/