+++
title= "[UE4]Occlusion Culling"
date= "2018-11-22T21:08:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["Occlusion Culling", "遮挡剔除", "场景优化", "Scene Optimization"]
+++

keywords: Occlusion Culling, 遮挡剔除, 场景优化, Scene Optimization

##### Working principle of Occlusion Culling

Unreal Engine 4 uses an automatic process for culling that uses Scene Depth and the bounds of an object.

When using the Wireframe viewmode, this is not a good method for testing if an object is occluded in UE4. You can use the (Editor only) console command `r.visualizeOccludedPrimitives 1` to view the occluded objects. This will render a green bounds box for any objects that are occluded. Adjusting the bounds scale will increase the green bounding box and can cause the mesh to be rendered even when it's not in view.

In the project settings you can disable Occlusion Culling completely if you need, but in most cases this is not needed.

There is an alternative method of occlusion in the engine that is not on by default. It's less strict than the currently default method. You can enable this by using the console command `r.HZBOcclusion 1`

This uses an approximation with occlusion culling. It will occlude the mesh dependent more on size and bounds scale than strictly on bounds scale. This can be useful in some instances, but problematic in others where it would cause meshes to be rendered that you wouldn't necessarily wan to be when hidden. This is largely why it's not on by default at the moment.

Using the first console command above is the best solution right now for debugging what's being occluded and what's not for the time being.

Original Text: How does object occlusion and culling work in UE4?  
https://answers.unrealengine.com/questions/312646/how-does-object-occlusion-and-culling-work-in-ue4.html

##### Occlusion Culling switch

Project Settings -> Engine -> Rendering -> Culling -> Occlusion Culling. It's checked by default.


***
`六盘山上高峰，红旗漫卷西风。今日长缨在手，何时缚住苍龙？` ----毛泽东《清平乐· 六盘山》
