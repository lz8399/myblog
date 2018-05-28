+++
title= "[UE4]Sharp Temporal AA"
date= "2018-05-17T14:44:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Temporal AA"]
+++

##### PC端开启Temporal AA

参考：
https://forums.unrealengine.com/development-discussion/rendering/106829-sharp-temporal-aa/page2?134157-Sharp-Temporal-AA=&viewfull=1

##### 移动端开启Temporal AA
Project Settings -》 Engine -》 Rendering -》 Default Settings -》 Anti-Aliasing Method 选择 TemporalAA；  
Project Settings -》 Engine -》 Rendering -》 Mobile -》 Mobile MSAA 选择 NO MSAA，并确保配置DefaultEngine.ini中r.MobileMSAA=0。

{{< alert danger >}}
4.19版本有bug，移动端无法开启Temporal AA，4.18没有问题。启用TemporalAA后，在Android设备上容易产生残影（转动屏幕或角色跑动时）。
{{< /alert >}}

***
`我希望有个如你一般的人`  
`如山间清爽的风`  
`如古城温暖的光`  
`从清晨到夜晚`  
`由山野到书房`  
`只要最后是你`  
`就好`  
`——张嘉佳 《从你的全世界路过》`