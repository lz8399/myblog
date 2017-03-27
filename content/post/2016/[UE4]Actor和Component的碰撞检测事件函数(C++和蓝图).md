---
title: "[UE4]Actor和Component的碰撞检测事件函数(CPP和蓝图)"
date: "2016-10-09T15:26:02+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

Actor
如果想在一个Actor发生碰撞时触发事件函数，那么重写Actor的两个函数之一：

    /** 
     *	Called when another actor begins to overlap this actor, for example a player walking into a trigger.
     *	For events when objects have a blocking collision, for example a player hitting a wall, see 'Hit' events.
     *	@note Components on both this and the other Actor must have bGenerateOverlapEvents set to true to generate overlap events.
     */
    Actor::OnActorBeginOverlap()


    /** 
     * Event when this actor bumps into a blocking object, or blocks another actor that bumps into it.
     * This could happen due to things like Character movement, using Set Location with 'sweep' enabled, or physics simulation.
     * For events when objects overlap (e.g. walking into a trigger) see the 'Overlap' event.
     *
     * @note For collisions during physics simulation to generate hit events, 'Simulation Generates Hit Events' must be enabled.
     * @note When receiving a hit from another object's movement (bSelfMoved is false), the directions of 'Hit.Normal' and 'Hit.ImpactNormal'
     * will be adjusted to indicate force from the other object against this object.
     */
    Actor::ReceiveHit()

如果不用重写函数的方式，也可以和注册事件来检测碰撞，例子：
先注册

    void UYourActorComponent::InitializeComponent()
    {
        FScriptDelegate Delegate;
        Delegate.BindUFunction(this, "OnActorBump");
        GetOwner()->OnActorHit.AddUnique(Delegate);
    }

函数体

    UCLASS(....)
    class UYourActorComponent : public UActorComponent
    {
    ....
        UFUNCTION()
        void OnActorBump(AActor* SelfActor, AActor* OtherActor, FVector NormalImpulse, const FHitResult& Hit);
    ....
    };



Component自身提供的检测函数有：

    UPrimitiveComponent::LineTraceComponent();
    UPrimitiveComponent::SweepComponent();
    UPrimitiveComponent::ComponentOverlapComponent();
    UPrimitiveComponent::OverlapComponent();

Component碰撞事件的注册方式如下：

    curItem->collMesh->OnComponentBeginOverlap.Add(const FScriptDelegate& Delegate);
    curItem->collMesh->OnComponentEndOverlap.Add(const FScriptDelegate& Delegate);



蓝图对应这两个函数的节点分别为：

    EventActorBeginOverlap
    EventHit

更多参考：

https://docs.unrealengine.com/latest/INT/Engine/Blueprints/UserGuide/Events/index.html#eventhit