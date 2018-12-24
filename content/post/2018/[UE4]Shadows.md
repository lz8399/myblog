+++
title= "[UE4]Shadows"
date= "2018-04-27T14:14:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Scene Optimization"]
+++

keywords：UE4、Shadows、Scene Optimization、阴影、场景优化

##### Cascaded Shadow Maps related

1，开启 `Dynamic Shadow Distance`  
测试用例： 500 个  Actor 同屏，摄像机高度4000，DirectionalLight 的属性`Dynamic Shadow Distance StationaryLight`（默认为0，表示关闭）的值要大于摄像机到Actor的直线距离（注意：是到每个Actor的直线距离，所以值尽量要设置的大一些），否则帧率从200 fps 下降到 100 fps。


##### 参考资料

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