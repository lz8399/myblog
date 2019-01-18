+++
title= "[UE4]Particle Emitter Related"
date= "2018-11-01T16:57:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

##### C++获取特效实例中的单个Emitter对象

UParticleSystemComponent 有个EmitterInstances属性，里面包含了特效中每个Emitter的相关信息：

    TArray<struct FParticleEmitterInstance*> EmitterInstances;

##### 粒子循环播放

打开特效编辑器 -》 选中要循环播放的粒子(Emitter) -》 Spawn -》修改 `Emitter Loops` 为0，表示循环播放。

***
`人生在世，两种事应该少干：用自己的嘴干扰别人的人生；靠别人的脑子思考自己的人生。`
