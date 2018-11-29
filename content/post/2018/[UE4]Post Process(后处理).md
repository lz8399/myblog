+++
title= "[UE4]Post Process(后处理)"
date= "2018-04-27T14:14:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Post Process"]
+++

##### 官方文档

Post Process Materials  
https://docs.unrealengine.com/en-us/Engine/Rendering/PostProcessEffects/PostProcessMaterials

Stylized Rendering Post Processing  
https://docs.unrealengine.com/en-us/Resources/Showcases/Stylized/PostProcessing

Post Processing Content Examples  
https://docs.unrealengine.com/en-us/Resources/ContentExamples/PostProcessing

1.2 - ShadingModel  
https://docs.unrealengine.com/en-us/Resources/ContentExamples/MaterialProperties/1_2

Post Processing Content Examples  
https://docs.unrealengine.com/en-us/Resources/ContentExamples/PostProcessing

Rendering Overview  
https://docs.unrealengine.com/en-us/Engine/Rendering/Overview

Post Process Effects  
https://docs-origin.unrealengine.com/latest/INT/Engine/Rendering/PostProcessEffects/index.html

PostProcessVolume的settings中各个属性对应的效果类型  
https://docs-origin.unrealengine.com/latest/INT/Engine/Rendering/PostProcessEffects/index.html#postprocesssettings


##### youtube教程

Unreal Engine 4 Tutorial - Post Process Effects  
https://www.youtube.com/watch?v=i6lYSXyUKRY

Unreal Engine 4 Beginner Tutorial Series - #34 Post Processing  
https://www.youtube.com/watch?v=i9bnPStLYfk

Unreal 4 Post Processing Volume Part 03 Colour Grading with LUT's  
https://www.youtube.com/watch?v=HR_Mj8o-tQ4

Ue4: Post Processing Volume - Adding/Controlling Ambient Occulsion  
https://www.youtube.com/watch?v=-u1uzJxa94Q

Ue4: Post Processing Volume - Bloom and Lens Flare  
https://www.youtube.com/watch?v=7CU5_gLIJBs


##### 移动端的Post Process Volume 问题

4.20打包安卓版时有个问题：`Post Process Volume` 添加了一个Post Process Materials，这个Material在PC端没有问题，但是在安卓上会遮挡整个摄像机。  
但不是每个Material都有这种问题，具体是Material中什么函数或选项导致这种问题，没详细验证过。

***
`抱必死的心，走永远的路。`