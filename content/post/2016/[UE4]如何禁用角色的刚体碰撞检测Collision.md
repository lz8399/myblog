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

另外一种方式：

    MyCharacter->GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
    
这种第二种方式，不会禁用CollisionComponent的碰撞（个人理解，具体未测试）。