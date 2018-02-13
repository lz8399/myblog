---
title: "[UE4]如何设置移动版本的材质质量"
date: "2016-10-21T22:13:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Mobile
---

Key：android、mobile、material、building、low quality

##### Rendering参数
现在版本的UE4编译android版本时，默认使用的是最高特效，如果想是为了低配设备编译，可以在Project Settings –》 Engine –》 Rendering -》Mobile中，去掉HDR和Shadowing
{{< figure src="/img/20161021-[UE4]如果设置移动版本的材质质量.jpg">}}

##### OpenGL和Vulkan版本选择
以Android版本为例：  
Project Settings -》 Platforms -》 Android -》 Build -》 Support OpenGL ES3.1。默认只使用OpenGL ES2。

##### 相关文档
Scalability Reference
https://docs.unrealengine.com/latest/INT/Engine/Performance/Scalability/ScalabilityReference/

Performance Guidelines for Mobile Devices  
https://docs.unrealengine.com/latest/INT/Platforms/Mobile/Performance/

Materials for Mobile Platforms
https://docs.unrealengine.com/latest/INT/Platforms/Mobile/Materials/

