---
title: "[UE4]蓝图播放序列帧(UAnimSequence)"
date: "2016-09-16T21:58:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

播放动画Anim的蓝图节点时Play Animation，左侧的判断节点(==)是自己定义的判断Character状态的枚举值，如果是死亡状态，则播放死亡动画。
只要是正常播放UAnimSequence，当播放完毕以后会自动停留在最后一帧，无需手动设置。

注意事项：
`1，这里是播放Anim，不是Montage。正常逻辑下，Montage不用手动执行，一般都是通过属性值(Speed)来动态驱动的。`
2，Play Animation是在Character对象中才能访问，如果在Character蓝图之外访问，需要先获得Character对象，然后再从Character对象节点中拉出Play Animation节点。

{{< figure src="/img/20160916-[UE4]蓝图播放序列帧(UAnimSequence).jpg">}}

