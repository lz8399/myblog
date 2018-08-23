+++
title= "[UE4]Movement相关的API"
date= "2016-06-19T17:33:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

##### 如何修改角色的最大移动速度

    if (UCharacterMovementComponent* Movement = MyCharacter->GetCharacterMovement())
    {
        Movement->MaxWalkSpeed *= 0.5;
    }
    
##### 如何修改角色的当前移动速度

Tick() 中执行：

    GetCharacterMovement()->Velocity = FVector(0.f, 500.f, 0.f);

##### 如何停止正在移动的Pawn

    AController::StopMovement()
    
##### 修改重力加速度(Gravity)

+ 编辑器中设置全局重力加速度  
Project Settings -》 Engine -》 Physics -》 Default Physics Settings -》 Default Gravity Z。

+ 运行时runtime期间设置全局重力加速度：

        AWorldSettings* MyWorldSetting=GetWorldSettings();
        MyWorldSetting->bGlobalGravitySet=true;
        MyWorldSetting->GlobalGravityZ = 900.f;

+ 设置单个角色的重力加速度（倍率）

        MyCharacter->GetCharacterMovement()->GravityScale = 100.f

