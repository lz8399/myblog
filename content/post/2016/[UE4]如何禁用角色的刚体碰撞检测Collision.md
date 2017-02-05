---
title: "[UE4]如何禁用角色的刚体碰撞检测Collision"
date: "2016-10-12T20:15:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

通常的做法是：

    MyCharacter->SetActorEnableCollision(false);

这样设置以后，角色就可以忽视一切障碍物或者刚体来进行移动了。

另外Mesh也提供了接口来禁用刚体，但是一般情况都是将刚体加载角色蓝图中，而不是加载角色的Mesh上，所以这种不适用常规情况。

    MyCharacter->GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);