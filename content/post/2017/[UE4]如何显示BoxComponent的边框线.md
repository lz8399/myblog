---
title: "[UE4]如何显示BoxComponent的边框线"
date: "2017-05-15T22:21:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

比如，在角色蓝图中创建个BoxCollision：
{{< figure src="/img/20170515-[UE4]如何显示BoxComponent的边框线/[UE4]如何显示BoxComponent的边框线-01.jpg">}}

在游戏运行过程中，box的边框是看不见的，如果想让边框可见，则不勾选Hidden in Game属性。对应的C++属性也是同名属性。
{{< figure src="/img/20170515-[UE4]如何显示BoxComponent的边框线/[UE4]如何显示BoxComponent的边框线-02.jpg">}}

游戏运行中的效果：
{{< figure src="/img/20170515-[UE4]如何显示BoxComponent的边框线/[UE4]如何显示BoxComponent的边框线-03.jpg">}}