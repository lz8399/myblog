+++
title= "[UE4]大规模场景的优化(Large Scale Scene Optimization)"
date= "2018-03-03T18:31:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["场景优化", "Scene Optimization"]
+++

keywords: 场景优化，Scene Optimization

Here are a few tips:

Start with dividing your project in logical smaller sub areas. Decide where you want more detail or what will be just background architecture.
- use less detail in background areas.
- the bigger your scene the more optimized it needs to be. Not just for performance but also for light map size or texture caching.

This brings us to the next problem: Lighting.
- you need to decide if you want to have baked or dynamic lighting. Baked lighting is better looking and more efficient to render but depending on how optimized your assets are you might end up with unmanageable light map sizes. So if you didn't really optimize all your assets then you may need to go to fully dynamic lighting.
- set your skybox / lighting / further away environment early because it affects the lighting in your scene and how every object will look at the end. 

Use sub-levels for each area.
- areas with more detail need additional sub levels for this detail. This isn't really a technical requirement but you might want to stream these small items in and out if needed. The best optimization is removing an object from the scene if it isn't visible. 

Optimization tips
- as a general advice: unreal always liked smaller objects over huge assets. Not just for light map sizes but also for collision and general handling. If you have 2 symmetrical building parts than mirror them in unreal and not in 3ds max.
- but​​​​​ watch out for your draw calls. An object with 10 material id's has 10 draw calls. With Arch Viz objects you can quickly have too many draw calls. Recommended are something like 1000-1500 draw calls in view. If you have 100 cars with 10 materials on each of them then that's almost all the draw calls you can have. (In Arch Viz you can probably go a bit higher with the draw calls as there is no game play happening that eats up your CPU performance. Draw calls happen on the CPU not GPU.)
- use cull distance volumes that automatically remove invisible objects according to their size.
- use foliage for vegetation. But remember: whatever that foliage is painted on needs to stay with this base mesh in the same level or you won't be able to modify it later on.
- use instancing as much as possible. Light poles, benches, windows, anything that is repeated will render a lot faster when instanced. It pays off a lot if these objects are optimized. You get away with a few high poly houses but you won't get away with 100 super expensive car meshes.
- don't forget collision if you want to move around in the scene. Often per poly collision is fine for ArchViz. You can set that in your player character for the entire scene.

Other than that it is just a matter of scale. You can have one house where you put a thousand little things in or you can have a small city with a thousand larger items. It will render the same speed if the detail is properly scaled up or down. You can even have both if you only render the small items when you actually see them.

##### 参考
UE4 for Large Scale Scenes.  
https://forums.unrealengine.com/development-discussion/architectural-and-design-visualization/1368939-ue4-for-large-scale-scenes

Distance Field Ambient Occlusion(距离场环境遮挡)  
https://docs.unrealengine.com/latest/INT/Engine/Rendering/LightingAndShadows/DistanceFieldAmbientOcclusion/index.html

【UnrealEngine4】距离场的使用技巧与应用  
https://zhuanlan.zhihu.com/p/29214784

Creating and Using LODs（创建LOD）  
https://docs.unrealengine.com/latest/INT/Engine/Content/Types/StaticMeshes/HowTo/LODs/

Setting Up Automatic LOD Generation（自动生成LOD）  
https://docs.unrealengine.com/latest/INT/Engine/Content/Types/StaticMeshes/HowTo/AutomaticLODGeneration/