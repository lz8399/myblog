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

其他参考：  
C++创建BoxCollision(BoxComponent)并注册Overlap和Hit事件回调函数  
https://dawnarc.com/2017/05/ue4c--%E5%88%9B%E5%BB%BAboxcollisionboxcomponent%E5%B9%B6%E6%B3%A8%E5%86%8Coverlap%E5%92%8Chit%E4%BA%8B%E4%BB%B6%E5%9B%9E%E8%B0%83%E5%87%BD%E6%95%B0/