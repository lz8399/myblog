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

1，Actor->SetActorLocation

    Actor->SetActorLocation()
	
2，AActor::AddActorWorldOffset(), AActor::AddActorLocalOffset()

{{< alert warning >}}
AddActorWorldOffset与AddActorLocalOffset区别：如果期望Actor沿着某个世界坐标系方向移动，那么使用AddActorWorldOffset并且参数为世界坐标系的DeltaLocation；如果期望Actor沿着当前Actor局部坐标系方向移动，那么使用AddActorLocalOffset并且参数为相对当前Actor的DeltaLocation Offset。
{{< /alert >}}

{{< alert danger >}}
如果使用AddActorWorldOffset或者AddActorLocalOffset移动Character，那么MovementMode必须设置为fly，否则当DeltaLocation较小时，角色会始终往下掉（即使禁用物理模拟）。UCharacterMovementComponent::SetMovementMode(EMovementMode::MOVE_Flying);
{{< /alert >}}

3，Velocity

    ACharacter->GetCharacterMovement()->Velocity += FVector(5.f, 5.f, 0.f);

4，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用：
    
    Controller->MoveTo();

5，将一个Controller（PlayerController或者AIController）possess到一个Actor上，然后调用

    GetWorld()->GetNavigationSystem()->SimpleMoveToLocation(Controller, DestLocation);

{{< alert danger >}}
注意：如果使用Controller->MoveTo或者使用NavigationSystem的Move函数，前提条件是你使用了Navigation组件并build了地形，否则无效。
{{< /alert >}}

6，APawn->AddMovementInput

    APawn->AddMovementInput(FVector WorldDirection, float ScaleValue = 1.0f, bool bForce = false);
    
其中WorldDirection是方向，ScaleValue是速率倍速，bForce表示是否忽略Controller中的IgnoreMoveInput属性值，强制移动。


7，UCharacterMovementComponent::AddImpulse

    void UCharacterMovementComponent::AddImpulse( FVector Impulse, bool bVelocityChange )

AddImpulse 一般用来做投掷、爆炸、击飞等物理效果。添加的是一个瞬间的力，之后就不需要每帧做处理了。
{{< alert danger >}}
注意：AddImpulse 作用对象一般都是 StaticMeshComponent ，而不能是 CollisionComponent，否则无效。且 StaticMeshComponent 要开启物理：SetSimulatePhysics(true) ，否则也无效。
{{< /alert >}}

8，UCharacterMovementComponent::AddForce

    void UCharacterMovementComponent::AddForce( FVector Force )

如果想让物体保持移动，需要每帧都执行AddForce()函数，也就说如果加速度是实时变化的，那么就可以用AddForce。
两者的区别可以参考：  
https://forums.unrealengine.com/showthread.php?29496-Addforce-and-addimpulse  
`AddForce accounts for delta time and should be used for applying force over more than one frame, AddImpulse does not account for delta time and should be used for single 'pushes', like from an explosion or being thrown by a player. The reason is that if you use AddForce for throwing or an explosion, how far the object moves depends on the framerate at the exact frame the force was applied, rather than being independent of framerate like AddImpulse is.`

参考：  
https://forums.unrealengine.com/showthread.php?29496-Addforce-and-addimpulse


9，UKismetSystemLibrary::MoveComponentTo

	FLatentActionInfo ActionInfo;
	ActionInfo.CallbackTarget = this;
	UKismetSystemLibrary::MoveComponentTo(TopDownCameraComponent, Location, Rotation, false, false, 1.f, true, EMoveComponentAction::Move, ActionInfo);
	
一般用来移动Actor身上的Component，例如CameraComponent等。支持平滑移动，可以设置移动到目标Location、Rotation过程的时长。

