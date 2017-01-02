+++
title= "[UE4]飞行模式中的加速减速问题"
date= "2016-07-18T21:27:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

CharacterMovement默认有一个加速效果（属性值为MaxAcceleration，默认为2048，表示加速率），如果MovementMode设置为Walking模式，当调用`Controller->StopMovement()`来立即停止移动；
但是Flying Mode时，即使不再执行`AddMovementInput()`，Actor仍然会继续滑行一段距离，如果希望此时立即停止不滑行，需要将减速速率（默认为0）设置为加速速率的大小：

    GetCharacterMovement()->BrakingDecelerationFlying = GetCharacterMovement()->MaxAcceleration;