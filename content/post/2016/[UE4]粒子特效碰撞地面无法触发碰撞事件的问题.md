---
title: "[UE4]粒子特效碰撞地面无法触发碰撞事件的问题"
date: "2016-10-09T01:22:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keyword：**UE4、Particle、Emitter、Collision、Hit、Event、Floor**

问题表现：粒子特效中有个事件类型为collision的Event Generator

{{< figure src="/img/20161009-[UE4]粒子特效碰撞地面无法触发碰撞事件的问题/[UE4]粒子特效碰撞地面无法触发碰撞事件的问题-01.jpg">}}
 
但是当粒子发生碰撞时（比如撞击地面时），并没有触发此Event。原因可能如下：

1，	碰撞的物体没有设置为static
{{< figure src="/img/20161009-[UE4]粒子特效碰撞地面无法触发碰撞事件的问题/[UE4]粒子特效碰撞地面无法触发碰撞事件的问题-02.jpg">}}

2，	碰撞方式没有设置default或者BlockAll
{{< figure src="/img/20161009-[UE4]粒子特效碰撞地面无法触发碰撞事件的问题/[UE4]粒子特效碰撞地面无法触发碰撞事件的问题-03.jpg">}}
 
3，	如果是4.15之前的版本，修改Config/DefaultEngine.ini中[/Script/Engine.Engine]节点下的参数bUseFixedFrameRate设置为true，删掉这个参数或者设为false即可：

`bUseFixedFrameRate=True`

这是UE4的一个bug，在4.15版本修复了：https://issues.unrealengine.com/issue/UE-37210

