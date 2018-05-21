+++
title= "[UE4]移动端材质与贴图问题"
date= "2018-03-16T13:10:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Mobile Material", "Mobile Texture"]
+++

Keywords：android、mobile、material、building、low quality


##### Rendering参数
现在版本的UE4编译android版本时，默认使用的是最高特效，如果想是为了低配设备编译，可以在Project Settings –》 Engine –》 Rendering -》Mobile中，去掉HDR和Shadowing
{{< figure src="/img/20180316-[UE4]移动端材质与贴图问题/[UE4]移动端材质与贴图问题-02.jpg">}}

##### OpenGL和Vulkan版本选择
以Android版本为例：  
Project Settings -》 Platforms -》 Android -》 Build -》 Support OpenGL ES3.1。默认只使用OpenGL ES2。

##### iOS版本材质丢失或马赛克的问题(Material Mosaic)
问题现象：  
在Mac上以ios渲染模式运行，材质丢失，打包到真机上运行，材质变成马赛克。

解决办法：  
打开材质蓝图，勾选Use Full Precision。
{{< figure src="/img/20180316-[UE4]移动端材质与贴图问题/[UE4]移动端材质与贴图问题-01.jpg">}}

参考自：  
https://answers.unrealengine.com/questions/211323/layered-landscape-material-on-mobile.html

##### 相关文档
Scalability Reference
https://docs.unrealengine.com/latest/INT/Engine/Performance/Scalability/ScalabilityReference/

Performance Guidelines for Mobile Devices  
https://docs.unrealengine.com/latest/INT/Platforms/Mobile/Performance/

Materials for Mobile Platforms
https://docs.unrealengine.com/latest/INT/Platforms/Mobile/Materials/


***
`只有诗人同圣徒才能相信，在沥青路上辛勤浇水会培养出百合花来。  ----毛姆`