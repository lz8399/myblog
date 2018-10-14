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

##### 飞行模式中的加速减速问题
CharacterMovement默认有一个加速效果（属性值为MaxAcceleration，默认为2048，表示加速率），如果MovementMode设置为Walking模式，当调用`Controller->StopMovement()`来立即停止移动；
但是Flying Mode时，即使不再执行`AddMovementInput()`，Actor仍然会继续滑行一段距离，如果希望此时立即停止不滑行，需要将减速速率（默认为0）设置为加速速率的大小：

    GetCharacterMovement()->BrakingDecelerationFlying = GetCharacterMovement()->MaxAcceleration;
    
##### 设置MovementMode时的注意事项
如果一个Actor被Spawn出来之后，其MovementMode默认状态是Walking，如果此时Spawn的位置在空中，在没有Controller对其Possess的情况下，其静止在空中，当Possess之后，MovementMode会自动变为Falling，如果想让其继续停留在空中(比如飞行类的角色)，此时再手动将其MovementMode设置为Flying。`绝对不能在possess之前设置，否则设置状态会被引擎修改掉。`

##### Controller.StopMovement()和MovementComponent.StopMovementImmediately()的区别
前者只执行：

    PathFollowingComp->AbortMove(*this, FPathFollowingResultFlags::MovementStop);

后者先执行：

    Velocity = FVector::ZeroVector;
    
接着再执行：

    PathFollowingComp->AbortMove(*this, FPathFollowingResultFlags::MovementStop);

##### NavigationSystem寻路相关的API
检测某个坐标点是否在navmesh内，即可以作为寻路的坐标点。
UNavigationSystem::TestPathSync 实例用法：

    UNavigationSystem* const NavSys = GetWorld()->GetNavigationSystem();
    const ANavigationData* NavData = NavSys->GetNavDataForProps(YourCharacter->GetNavAgentPropertiesRef());
    FPathFindingQuery Query1(YourCharacter, *NavData, YourCharacter->GetNavAgentLocation(), TestLocation);
    bool qrs1 = NavSys->TestPathSync(Query1);


UNavigationSystem::FindPathSync也可以判断，但是他会返回寻路结果，效率上没有TestPathSync快。
其他的API还有：

    UNavigationSystem::ProjectPointToNavigation