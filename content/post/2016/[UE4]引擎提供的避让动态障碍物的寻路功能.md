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

但这里有个问题，胶囊体上下部分是半球形的，整个胶囊体与地面接触时只有一个点，对NavMesh来说不是一个障碍物，如果要让物体成为NavMesh中的障碍物，那么需要增加一个box类型的刚体：
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-04.jpg)

然后再设置这个box的属性值Dynamic Obstacle为true：
![This is an image](/img/20160801-[UE4]引擎提供的避让动态障碍物的寻路功能/[UE4]引擎提供的避让动态障碍物的寻路功能-05.jpg)

这样当有box collistion的角色在场景移动时，NavMesh会实时更新。这种操作可能对服务端性能影响较大，具体还没测过。