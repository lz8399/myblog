+++
title= "[UE4]移动端材质与贴图问题"
date= "2018-03-16T13:10:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Mobile Material", "Mobile Texture"]
+++

##### iOS版本材质丢失或马赛克的问题(Material Mosaic)
问题现象：  
在Mac上以ios渲染模式运行，材质丢失，打包到真机上运行，材质变成马赛克。

解决办法：  
打开材质蓝图，勾选Use Full Precision。
{{< figure src="/img/20180316-[UE4]移动端材质与贴图问题/[UE4]移动端材质与贴图问题-01.jpg">}}

参考自：  
https://answers.unrealengine.com/questions/211323/layered-landscape-material-on-mobile.html

***
`只有诗人同圣徒才能相信，在沥青路上辛勤浇水会培养出百合花来。  ----毛姆`