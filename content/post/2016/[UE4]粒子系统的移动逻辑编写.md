---
title: "[UE4]粒子系统的移动逻辑编写"
date: "2016-09-20T20:06:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、粒子特效、粒子、Particle、Emitter、移动、Move

1，	先在资源浏览器中新建一个蓝图，类型选择Actor即可
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-01.jpg">}}

{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-02.jpg">}}
 

2，	打开actor蓝图，点击右上角的Add Component，类型选择Particle System：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-03.jpg">}} 

添加之后，默认会添加到DefaultSceneRoot之下：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-04.jpg">}}
 
DefaultSceneRoot我们不需要。鼠标左键按住ParticleSytem节点不放，拖拽到DefaultSceneRoot节点之中，这样DefaultSceneRoot就会被替换为ParticleSystem：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-05.jpg">}}

3，	设置ParticleSystem，选择我们做好的粒子特效：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-06.jpg">}}

4，添加ProjectileMovement：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-07.jpg">}}

{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-08.jpg">}}

5，设置ProjectileMovement参数：设置初始速度和最大速度，如果不需要重力影响，可以将Projectile Gravity Scale设置为0。
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-09.jpg">}}

ProjectileMovement的速度可以先设置为0，在蓝图事件中对速度进行，逻辑如下（在Actor蓝图中编辑）：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-10.jpg">}}
 


##### 如果碰到Actor无法移动的问题，原因可能如下：

1，	static mesh没有设置为Movable。由于我们这里是粒子，所以没有static mesh，如果有，设置如下：
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-11.jpg">}}

2，	速率Velocity设置太小。所以上面我么对Normalize出来的Vector乘以了300。
{{< figure src="/img/20160920-[UE4]粒子系统的移动逻辑编写/[UE4]粒子系统的移动逻辑编写-12.jpg">}}
 
