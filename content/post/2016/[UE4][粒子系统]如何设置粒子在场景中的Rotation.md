---
title: "[UE4][粒子系统]如何设置粒子在场景中的Rotation"
date: "2016-10-06T18:48:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

如果想在游戏场景中控制粒子特效的Rotation，需要勾选发射器**Required**组件中的`Use Local Space`选项，否则无论设置rotation值多少，其旋转角度始终是默认的初始值。
（查看大图，请复制图片链接在新窗口中打开）

{{< figure src="/img/20161006-[UE4][粒子系统]如何设置粒子在场景中的Rotation.jpg">}}

