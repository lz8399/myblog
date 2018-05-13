---
title: "[UE4]PointLight点光源的衰减参数"
date: "2016-10-20T13:46:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Linghting
---

要想以较小的Intensity（光照强度）来获得较大的光照面积（或者光照亮度），影响的参数有两个

+ **Attenuation Radius**（衰减半径）：衰减半径越大，光照区域越大  
+ **Use Inverse Squared Falloff**（是否启用平方反差衰减）：如果启用，则会以真实世界的光照效果来模拟物体与光源距离的不同而光照效果衰减变化的效果。如果不启用，则能增大光照区域。如果场景中有高度雾，开启此属性后，灯光的半径设置的再大，光照范围也不会有明显增大。

参数示例：
{{< figure src="/img/20161020-[UE4]PointLight点光源的衰减参数/[UE4]PointLight点光源的衰减参数-01.jpg">}} 

效果：
{{< figure src="/img/20161020-[UE4]PointLight点光源的衰减参数/[UE4]PointLight点光源的衰减参数-02.jpg">}}

官方文档：
https://docs.unrealengine.com/latest/INT/Resources/ContentExamples/Lighting/4_2/index.html

{{< figure src="/img/20161020-[UE4]PointLight点光源的衰减参数/[UE4]PointLight点光源的衰减参数-03.jpg">}}

***
`先知先觉者胜，后知后觉者平，不知不觉者败。`