---
title: "[UE4]如何制作RTS游戏中的角色脚下圆环"
date: "2016-06-12T10:24:40+08:00"
categories:
- UnrealEngine4
tags:
- RTS
- UE4
---


1，准备好贴图
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-1.jpg)

2，新建一个材质蓝图
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-2.jpg)

3，在蓝图中新建个Texture Sample节点，并设置为之前准备的贴图
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-3.jpg)

4，将材质的Blend Mode设置为Translucent半透明模式
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-4.jpg)

5，设置好材质的BaseColor和Opacity
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-5.jpg)

6，然后新建一个Actor蓝图
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-6.jpg)

![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-7.jpg)

![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-8.jpg)

7，在actor蓝图中新建个Scene组件
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-9.jpg)

8，将新建个Scene组件拖拽到Root根节点中，以替换原来默认根节点
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-11.jpg)

10，然后再新建一个StaticMesh组件
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-12.jpg)

11，然后将这个StaticMesh组件的Mesh设置为一个地砖形状的模型
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-13.jpg)

12，同时讲StaticMesh的材质设置为之前新建个材质
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-14.jpg)

13，然后将actor蓝图设置为Movable
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-15.jpg)

14，这样设置完成了，之后就可以将这个actor蓝图spawn到场景中并attach到人物的身上，并设置后相对坐标即可
![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-16.jpg)

![This is an image](/img/20160612-[UE4]如何制作RTS游戏中的角色脚下圆环/[UE4]如何制作RTS游戏中的角色脚下圆环-17.jpg)