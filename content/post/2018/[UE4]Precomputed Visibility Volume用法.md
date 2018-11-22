+++
title= "[UE4]Precomputed Visibility Volume用法"
date= "2018-03-03T11:22:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["预计算可视性", "场景优化", "Scene Optimization"]
+++

keywords: 预计算可视性，场景优化，Scene Optimization

Precomputed visibility not working on Mobile/MobilePIE  
https://answers.unrealengine.com/questions/406345/precomputed-visibility-not-working-on-mobilemobile.html

PRECOMPUTED VISIBILITY VOLUMES  
http://timhobsonue4.snappages.com/culling-precomputed-visibility-volumes

UE4在场景中使用预计算可视性(PrecomputedVisibility)  
https://blog.csdn.net/jiangdengc/article/details/57421898

{{< alert danger >}}
Precomputed Visibility Volume并不适用于FPS游戏，因为FPS游戏摄像机转动非常剧烈频繁，后台预计算可视性的数据切换的计算也非常大，不一定能提升性能。
{{< /alert >}}

##### How does object occlusion and culling work in UE4?

Unreal Engine 4 uses an automatic process for culling that uses Scene Depth and the bounds of an object.

When using the Wireframe viewmode, this is not a good method for testing if an object is occluded in UE4. You can use the (Editor only) console command r.visualizeOccludedPrimitives 1 to view the occluded objects. This will render a green bounds box for any objects that are occluded. Adjusting the bounds scale will increase the green bounding box and can cause the mesh to be rendered even when it's not in view.

In the project settings you can disable Occlusion Culling completely if you need, but in most cases this is not needed.

There is an alternative method of occlusion in the engine that is not on by default. It's less strict than the currently default method. You can enable this by using the console command r.HZBOcclusion 1

This uses an approximation with occlusion culling. It will occlude the mesh dependent more on size and bounds scale than strictly on bounds scale. This can be useful in some instances, but problematic in others where it would cause meshes to be rendered that you wouldn't necessarily wan to be when hidden. This is largely why it's not on by default at the moment.

Using the first console command above is the best solution right now for debugging what's being occluded and what's not for the time being.

原文：  
https://answers.unrealengine.com/questions/312646/how-does-object-occlusion-and-culling-work-in-ue4.html

##### 

***
`早知如此绊人心，何如当初莫相识。----李白《秋风词》`