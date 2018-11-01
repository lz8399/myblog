+++
title= "[UE4]Particle Emitter 粒子特效相关"
date= "2018-11-01T16:57:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

##### C++获取特效实例中的单个Emitter对象

UParticleSystemComponent 有个EmitterInstances属性，里面包含了特效中每个Emitter的相关信息：

    TArray<struct FParticleEmitterInstance*> EmitterInstances;

