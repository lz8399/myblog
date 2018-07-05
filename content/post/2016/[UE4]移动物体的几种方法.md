---
title: "[UE4]移动物体的几种方法"
date: "2016-06-17T13:17:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

keywords: UE4、Movement

作者：@玄冬Wong

1，Actor->SetActorLocation

    Actor->SetActorLocation()

2，Velocity

    ACharacter->GetCharacterMovement()->Velocity += FVector(5.f, 5.f, 0.f);

3，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用：
    
    Controller->MoveTo();

4，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用

    GetWorld()->GetNavigationSystem()->SimpleMoveToLocation(Controller, DestLocation);

{{< alert danger >}}
注意：如果使用Controller->MoveTo或者使用NavigationSystem的Move函数，前提条件是你使用了Navigation组件并build了地形，否则无效。
{{< /alert >}}

5，APawn->AddMovementInput

    APawn->AddMovementInput(FVector WorldDirection, float ScaleValue = 1.0f, bool bForce = false);
    
其中WorldDirection是方向，ScaleValue是速率倍速，bForce表示是否忽略Controller中的IgnoreMoveInput属性值，强制移动。


6，UCharacterMovementComponent::AddImpulse

    void UCharacterMovementComponent::AddImpulse( FVector Impulse, bool bVelocityChange )

AddImpulse一般用来做投掷、爆炸、击飞等物理效果。添加的是一个瞬间的力，之后就不需要每帧做处理了。
{{< alert warning >}}
以实现一个击飞效果为例，要有明显击飞效果，Impulse 值要2000以上，且 bVelocityChange 设置为 true 。
{{< /alert >}}

7，UCharacterMovementComponent::AddForce

    void UCharacterMovementComponent::AddForce( FVector Force )

如果想让物体保持移动，需要每帧都执行AddForce()函数，也就说如果加速度是实时变化的，那么就可以用AddForce。
两者的区别可以参考：  
https://forums.unrealengine.com/showthread.php?29496-Addforce-and-addimpulse  
`AddForce accounts for delta time and should be used for applying force over more than one frame, AddImpulse does not account for delta time and should be used for single 'pushes', like from an explosion or being thrown by a player. The reason is that if you use AddForce for throwing or an explosion, how far the object moves depends on the framerate at the exact frame the force was applied, rather than being independent of framerate like AddImpulse is.`

参考：  
https://forums.unrealengine.com/showthread.php?29496-Addforce-and-addimpulse


8，UKismetSystemLibrary::MoveComponentTo

	FLatentActionInfo ActionInfo;
	ActionInfo.CallbackTarget = this;
	UKismetSystemLibrary::MoveComponentTo(TopDownCameraComponent, Location, Rotation, false, false, 1.f, true, EMoveComponentAction::Move, ActionInfo);
	
一般用来移动Actor身上的Component，例如CameraComponent等。支持平滑移动，可以设置移动到目标Location、Rotation过程的时长。