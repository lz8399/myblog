---
title: "[UE4][粒子系统]无延迟的立即播放特效"
date: "2016-09-18T11:59:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keywords：**Warmup Time、no delay、at once、Particle System**

默认播放特效时，会有一秒的延迟，如果想让粒子生成后立即播放，需要进行以下设置：  
1，点点击例子系统编辑界面最右侧的黑色空闲区域
{{< figure src="/img/20160918-[UE4][粒子系统]无延迟的立即播放特效/[UE4][粒子系统]无延迟的立即播放特效-01.jpg">}} 

2，然后在Detail面板中找到Warmup Time参数，修改为1。默认为0
{{< figure src="/img/20160918-[UE4][粒子系统]无延迟的立即播放特效/[UE4][粒子系统]无延迟的立即播放特效-02.jpg">}}




