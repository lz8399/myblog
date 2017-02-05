---
title: "[UE4]移动物体的几种方法"
date: "2016-06-17T13:17:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

1，

    Actor->SetActorLocation()

2，

    ACharacter->GetCharacterMovement()->Velocity += FVector(5.f, 5.f, 0.f);

3，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用：
    
    Controller->MoveTo();

4，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用

    GetWorld()->GetNavigationSystem()->SimpleMoveToLocation(Controller, DestLocation);

前提条件是你使用了Navigation组件并build了地形

5，

    APawn->AddMovementInput(FVector WorldDirection, float ScaleValue = 1.0f, bool bForce = false);
    
其中WorldDirection时方向，ScaleValue是速率倍速，bForce是忽略Controller中的IgnoreMoveInput属性值，强制移动。

