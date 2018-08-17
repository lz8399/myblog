+++
title= "[UE4]物理和刚体相关的注意事项(Simulate Physics and RigidBody)"
date= "2018-07-23T00:27:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Velocity", "AddImpulse", "Simulate Physics", "Collision"]
+++

##### UProjectileMovementComponent相关

官方第一人称射击模版项目中，是在构造函数中就设置好了速度：

	ProjectileMovement = CreateDefaultSubobject<UProjectileMovementComponent>(TEXT("ProjectileComp"));
	ProjectileMovement->UpdatedComponent = CollisionComp;
	ProjectileMovement->InitialSpeed = 3000.f;
	ProjectileMovement->MaxSpeed = 3000.f;
	ProjectileMovement->bRotationFollowsVelocity = true;
	ProjectileMovement->bShouldBounce = true;

两个问题：

1. 如何停止移动；
2. 如何在运行时期间修改速度；

问题1解决方法：  
默认情况下，Actor spawn之后，就会受到 ProjectileMovement 影响立即移动，如何在 Spawn 之后马上停止移动：

	ProjectileMovement->Deactivate();

问题2解决方法：  
如何在 Spawn 之后修改 Speed，两种方式：

	UProjectileMovementComponent->SetVelocityInLocalSpace(FVector NewVelocity);
	
或者

	UProjectileMovementComponent->Velocity = NewVelocity;
	
{{< hl-text blue >}}
前者速度方向是相对于 UProjectileMovementComponent本地坐标系 的相对Rotation，后者速度方向是相对于世界坐标系的绝对Rotation。
{{< /hl-text >}}

{{< alert danger >}}
注意：当使用 UProjectileMovementComponent 后，UPrimitiveComponent::SetSimulatePhysics() 启用物理会与 ProjectileMovement 冲突。如果要使用物理，那么只能去掉 UProjectileMovementComponent ，使用 Add Impulse 来代替。
{{< /alert>}}

参考：  
Simulate Physics and Projectile Movement Component  
https://answers.unrealengine.com/questions/736999/simulate-physics-and-projectile-movement-component.html

##### 模拟物理时StaticMesh和CollisionComponent冲突
记住：{{< hl-text red >}}StaticMesh自带刚体(RigidBody)，并能执行碰撞(Collision)相关逻辑。{{< /hl-text >}}  
比如新建一个 Actor，并在该 Actor 内部创建了一个 BoxComponent ，然后再创建一个 StaticMeshComponent 并 Attach 到 BoxComponent 上。  
如果不模拟物理，那么没有问题，一旦模拟物理并执行 AddImpulse 时，就会出问题。

现象：  
如果只对 StaticMeshComponent 执行击飞，那么 BoxComponent 会停在原地，如果对 BoxComponent 击飞： `BoxComponent->BodyInstance.AddImpulse()` ，那么 StaticMeshComponent 不会动。

解决办法：  
直接使用 StaticMeshComponent Collision ，不用与 Col1isionComponent 附加。


##### 如何处理发射刚体与角色刚体冲突

问题现象：  
当角色的`CollisionComponent`半径较大时，此时想在角色面前发射(`AddImpulse`)一个`Simulate Physics`的`StaticMeshActor`，但是当这个 Actor 刚发射之前，其刚体正好和角色的刚体相互影响，导致 Actor 没能按预定方向和速度运动。

解决办法：  
减小角色刚体半径，或者发射点放在刚体半径以外。（{{< hl-text red >}}如果仅仅是这样，那我写这篇文章干嘛。。。{{< /hl-text >}}）

正确方式：将`StaticMesh`的`CollisionType`设置为`PhysicsOnly`

	StaticMeshComp = CreateDefaultSubobject<UStaticMeshComponent>(TEXT("StaticMeshComp"));
	StaticMeshComp->SetCollisionEnabled(ECollisionEnabled::Type::PhysicsOnly);
    
{{< alert success >}}
4.16版本存在这种问题，但是最新4.20.1版本，即使放射物体在角色 CapsuleComponent 内部，且 CapsuleComponent 的 Object Response 对发射物体为 Block，发射时物体也不会存在乱窜的问题，不知是不是引擎把这种情况自动处理了。4.16到4.20之间的版本是否仍然存在这个问题，没有测试过。
{{< /alert >}}
	
##### 不使用 MovementComponent 情况下设置 Gravity 大小

MovementComponent 有个属性`Gravity Scale`来设置重力大小。  
假设一个 Actor 如果没有添加 MovementComponent ，只有一个 StaticMeshComponent ，此时 StaticMeshComponent 模拟物理时，其重力加速度较小，这种情况下有没办法设置重力加速度大小？方式如下：

	StaticMeshComp->SetSimulatePhysics(true);
	StaticMeshComp->AddImpulse(SpeedInWorld);

然后在 Tick 函数中每帧设置：

	FVector Velocity = StaticMeshComp->GetPhysicsLinearVelocity();
	Velocity.Z -= 100.f;
	StaticMeshComp->SetPhysicsLinearVelocity(Velocity);
	
说明：`GetPhysicsLinearVelocity` 默认为0，这里修改成 -100.f 的重力下降速率，
	