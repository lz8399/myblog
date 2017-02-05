---
title: "[UE4]粒子发射器的碰撞事件(Particle Collision Event)"
date: "2016-10-10T11:32:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keyword：**Particle、Emitter、Collision、Event、Dispathch、Blueprint、C++**

先保证粒子发射器中有碰撞检测事件：类型为Collision的Event Generator
{{< figure src="/img/20161010-[UE4]粒子发射器的碰撞事件(Particle Collision Event)/[UE4]粒子发射器的碰撞事件(Particle Collision Event)-01.jpg">}}

#### 蓝图方式：
Spawn创建粒子之后，绑定事件OnParticleCollide，然后新建一个自定义事件（图中命令为CustomEvent_0），然后就可以在这个事件中获取碰撞的坐标等信息了。
{{< figure src="/img/20161010-[UE4]粒子发射器的碰撞事件(Particle Collision Event)/[UE4]粒子发射器的碰撞事件(Particle Collision Event)-02.jpg">}}

注意：`这里的CumtomEvent_0无法单独创建出来，否则就是一个没有任何参数的普通custom event，必须从Bind Event to OnParticleCollide节点中拖拽出来`
{{< figure src="/img/20161010-[UE4]粒子发射器的碰撞事件(Particle Collision Event)/[UE4]粒子发射器的碰撞事件(Particle Collision Event)-03.jpg">}}


#### C++方式：

    UParticleSystemComponent* PSC = UGameplayStatics::SpawnEmitterAtLocation(MyGameMode->GetWorld(), SkillParticle_1004, Location, FRotator::ZeroRotator, true);

    FScriptDelegate Delegate;
    Delegate.BindUFunction(MyCharacter, "OnParticleHit");
    PSC->OnParticleCollide.Add(Delegate);

碰撞回调事件的函数签名：

    UFUNCTION()
            void OnParticleHit(FName EventName, float EmitterTime, int32 ParticleTime, FVector Location, FVector Velocity, FVector Direction, FVector Normal, FName BoneName, UPhysicalMaterial* PhysMat);
		
其中的Location就是撞击的坐标
