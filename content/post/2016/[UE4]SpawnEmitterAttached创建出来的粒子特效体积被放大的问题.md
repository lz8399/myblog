---
title: "[UE4]SpawnEmitterAttached创建出来的粒子特效体积被放大的问题"
date: "2016-10-14T21:54:02+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

问题表现：
使用UGameplayStatics::SpawnEmitterAttached创建的粒子尺寸大小异常，变得非常大，比SpawnEmitterAtLocation()创建出来的粒子大差不多六七倍。

解决版本：

    UParticleSystemComponent::bAbsoluteScale = true;

例子：

    UParticleSystemComponent* PSC = UGameplayStatics::SpawnEmitterAttached(ParticleTemplate, Unit->GetMesh());
    PSC->SetAbsolute(false, false, true);