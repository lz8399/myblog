+++
title= "[UE4]Controller.StopMovement()和MovementComponent.StopMovementImmediately()的区别"
date= "2016-10-01T23:46:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

Controller.StopMovement()和MovementComponent.StopMovementImmediately()的区别
前者只执行：

    PathFollowingComp->AbortMove(*this, FPathFollowingResultFlags::MovementStop);

后者先执行：

    Velocity = FVector::ZeroVector;
    
接着再执行：

    PathFollowingComp->AbortMove(*this, FPathFollowingResultFlags::MovementStop);