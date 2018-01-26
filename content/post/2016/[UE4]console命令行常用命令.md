---
title: "[UE4]console命令行常用命令"
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
	

https://docs-origin.unrealengine.com/latest/INT/Engine/Performance/StatCommands/