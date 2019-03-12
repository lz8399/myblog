+++
title= "[UE4]Shadows"
date= "2018-04-27T14:14:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Scene Optimization", "Shadow Optimization"]
+++

keywords：UE4, Shadow Optimization, Scene Optimization, 阴影, 场景, 优化

### Cascaded Shadow Maps related

##### Enable Dynamic Shadow Distance

Test Case: 500 Actors are rendering in screen, Camera height is 4000, DirectionalLight's property `Dynamic Shadow Distance StationaryLight` (Default value is 0, which means disabled) should be larger than the straight-line distance from Camera to Actor (Beacause the distance need to cover all Actors, so the distance would be better be larger ), otherwise frame rate would drop down from 200 fps to 100 fps.

### How to Cast Shadow by Camera Distance

Tow factors

+ RayTraced Distance Field Soft Shadows
+ Scalability of Shadow

##### RayTraced Distance Field Soft Shadows

1. Project Settings -> Engine -> Rendering -> Lighting -> enable `Generate Mesh Distance Fields` (Need to restart Editor)
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-00.jpg">}}

2. Modify DirectionalLight's properties: `DistanceField Shadow Distance` and `RayTraced DistanceField Shadows`
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-01.jpg">}}
Effect  
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-02.jpg">}}

##### Relationship between DistanceField Shadow Distance & Dynamic Shadow Distance

+ Stationary
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-03.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-04.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-05.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-06.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-07.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-08.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-09.jpg">}}

+ Moveable
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-10.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-11.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-12.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-13.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-14.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-15.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-16.jpg">}}

Reference:RayTraced Distance Field Soft Shadows  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/RayTracedDistanceFieldShadowing

##### Scalability of Shadow

+ Cinematic
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-17.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-18.jpg">}}

+ Medium
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-19.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-20.jpg">}}

+ Low
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-21.jpg">}}
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-22.jpg">}}

Scalability Reference  
https://docs.unrealengine.com/en-US/engine/performance/scalability/scalabilityreference

##### How to cast character shadow on mobile device

**1st way: Movable Directional Light**

{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-23.jpg">}}

How to Enable Dynamic Shadows & Correct Reflection Maps on Mobile  
https://forums.unrealengine.com/development-discussion/android-development/41661-tip-how-to-enable-dynamic-shadows-correct-reflection-maps-on-mobile

Lighting for Mobile Platforms  
https://docs.unrealengine.com/latest/INT/Platforms/Mobile/Lighting/

4.7 release mobile shadows  
https://answers.unrealengine.com/questions/180482/47-release-mobile-shadows.html

**2nd way: Stationary Directional Light**  
Enable `Cast Modulated Shadows`
{{< figure src="/img/20180427-[UE4]Shadows/[UE4]Shadows-24.jpg">}}


### Reference

Dynamic Scene Shadows  
https://docs.unrealengine.com/en-us/Resources/ContentExamples/DynamicSceneShadows

Cascaded Shadows  
https://docs.unrealengine.com/en-us/Platforms/Mobile/Lighting/HowTo/CascadedShadow

RayTraced Distance Field Soft Shadows  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/RayTracedDistanceFieldShadowing

Shadow Casting  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/Shadows

***
`人会长大三次。第一次是在发现自己不是世界中心的时候。第二次是在发现即使再怎么努力，终究还是有些事令人无能为力的时候。第三次是在，明知道有些事可能会无能为力，但还是会尽力争取的时候。`