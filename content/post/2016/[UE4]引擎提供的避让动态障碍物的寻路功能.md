---
title: "[UE4]引擎提供的避让动态障碍物的寻路功能"
date: "2016-08-01T23:06:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

1，设置NavigationMesh的Runtime Generation为Dynamic
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-01.jpg)

2，设置胶囊体为动态障碍物。  
先选中胶囊体
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-02.jpg)

再勾选Dynamic Obstacle（默认是勾选的）
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-03.jpg)

##### Epic官方讲解的动态避让AI方案

Dynamic Navigation Mesh  
https://answers.unrealengine.com/questions/223395/dynamic-navigation-mesh.html

Unreal Engine 4 Support Twitch Broadcast: AI  
https://www.youtube.com/watch?v=7LaazCv4rB0


##### Static Mesh 动态遮挡

添加一个box类型的刚体：
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-04.jpg)

然后再设置这个box的属性值Dynamic Obstacle为true：
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-05.jpg)

这样当有box collistion的角色在场景移动时，NavMesh会实时更新。  
如果针对Character也使用这种方式，那么Character的移动只能通过SetActorLocation()处理，MavigateSystem的MoveTo接口会失效。

