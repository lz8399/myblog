---
title: "[UE4]用C++如何创建Box Collision"
date: "2016-08-03T15:53:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

在蓝图中直接编辑添加Box Collision是这样的：
![This is an image](/img/20160803-[UE4]用C++如何创建Box Collision.jpg)

如果用C++，则如下：

    UBoxComponent* CollisionMesh = CreateDefaultSubobject<UBoxComponent>(TEXT("TestCollision"));
    CollisionMesh->SetBoxExtent(FVector(32.f, 32.f, 96.f));
    CollisionMesh->bDynamicObstacle = true;

    CollisionMesh->SetupAttachment(GetRootComponent());
    
注：
`使用CreateDefaultSubobject必须在构造函数中`，如果是其他成员函数，则形式为
UBoxComponent* MyNewBox = NewObject<UBoxComponent>(this);
这里的this是一个Character指针。但这样有个问题：NewObject非构造函数中创建的Box无法及时更新NavMesh，也就是说该box在NavMesh不会被当作障碍物。
