+++
title= "[UE4]Movement与Navigation相关的API"
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
    
**4.20版本**获取`NavigationSystem`方法：

    UNavigationSystemV1* UNavigationSystemV1::GetNavigationSystem(UObject* WorldContextObject);
	
或者：

	UNavigationSystemV1* NavSys = FNavigationSystem::GetCurrent<UNavigationSystemV1>(GetWorld());
	

获取指定坐标投射到NavMesh上的坐标；获取指定半径内可以行走的NavMesh的坐标点（随机获取）（4.20及之前老版本）：

UNavigationSystem.h：

    /** Project a point onto the NavigationData */
	UFUNCTION(BlueprintPure, Category = "AI|Navigation", meta = (WorldContext = "WorldContextObject", DisplayName = "ProjectPointToNavigation", ScriptName = "ProjectPointToNavigation"))
	static bool UNavigationSystemV1::K2_ProjectPointToNavigation(UObject* WorldContextObject, const FVector& Point, FVector& ProjectedLocation, ANavigationData* NavData, TSubclassOf<UNavigationQueryFilter> FilterClass, const FVector QueryExtent = FVector::ZeroVector);

	/** Generates a random location reachable from given Origin location.
	 *	@return Return Value represents if the call was successful */
	UFUNCTION(BlueprintPure, Category = "AI|Navigation", meta = (WorldContext = "WorldContextObject", DisplayName = "GetRandomReachablePointInRadius", ScriptName = "GetRandomReachablePointInRadius"))
	static bool UNavigationSystemV1::K2_GetRandomReachablePointInRadius(UObject* WorldContextObject, const FVector& Origin, FVector& RandomLocation, float Radius, ANavigationData* NavData = NULL, TSubclassOf<UNavigationQueryFilter> FilterClass = NULL);

	/** Generates a random location in navigable space within given radius of Origin.
	 *	@return Return Value represents if the call was successful */
	UFUNCTION(BlueprintPure, Category = "AI|Navigation", meta = (WorldContext = "WorldContextObject", DisplayName = "GetRandomPointInNavigableRadius", ScriptName = "GetRandomPointInNavigableRadius"))
	static bool UNavigationSystemV1::K2_GetRandomPointInNavigableRadius(UObject* WorldContextObject, const FVector& Origin, FVector& RandomLocation, float Radius, ANavigationData* NavData = NULL, TSubclassOf<UNavigationQueryFilter> FilterClass = NULL);
	
另外两个函数（4.20、4.21版本的非shipping打包模式可用，不知官方会不会在后续版本定为正式版的API）：

    bool ProjectPointToNavigation(const FVector& Point, FNavLocation& OutLocation, const FVector& Extent = INVALID_NAVEXTENT, const FNavAgentProperties* AgentProperties = NULL, FSharedConstNavQueryFilter QueryFilter = NULL);
    
    bool ProjectPointToNavigation(const FVector& Point, FNavLocation& OutLocation, const FVector& Extent = INVALID_NAVEXTENT, const ANavigationData* NavData = NULL, FSharedConstNavQueryFilter QueryFilter = NULL) const;
	
`K2_ProjectPointToNavigation`用法：

	FVector SourceLoc(1000.f, 1000.f, 100.f);
	FVector DestLoc;
	
	if (UNavigationSystemV1* NavSys = FNavigationSystem::GetCurrent<UNavigationSystemV1>(world))
	{
		if (ANavigationData* NavData = NavSys->GetDefaultNavDataInstance(FNavigationSystem::DontCreate))
		{
			NavSys->K2_ProjectPointToNavigation(world, SourceLoc, DestLoc, NavData, nullptr);
		}
	}
	
##### Difference between GetRandomReachablePointInRadius and GetRandomPointInNavigableRadius

{{< alert info >}}
OK, after some investigations and tests. I think I've got the idea.

So bool UNavigationSystem::GetRandomPointInNavigableRadius(const FVector& Origin, float Radius, FNavLocation& ResultLocation, ANavigationData* NavData, FSharedConstNavQueryFilter QueryFilter) const

will return a point on navmesh if succeed, but it doesn't check whether the point is on a connected navmesh which the Origin (first parameter) is on.

So bool UNavigationSystem::GetRandomReachablePointInRadius(const FVector& Origin, float Radius, FNavLocation& ResultLocation, ANavigationData* NavData, FSharedConstNavQueryFilter QueryFilter) const

will return a point on navmesh if succeed, and it will make sure the point in on a connected navmesh with the Origin.

So if the Origin is off navmesh and we want to find a point on navmesh, we need to use GetRandomPointInNavigableRadius.

If the Origin is on navmesh and we want to find a point to move to, we can use GetRandomReachablePointInRadius.
{{< /alert >}}

Reference: What's the difference between GetRandomReachablePointInRadius and GetRandomPointInNavigableRadius? In which case we should use which.  
https://answers.unrealengine.com/questions/796996/whats-the-difference-between-getrandomreachablepoi.html?sort=oldest
    
##### 寻路移动结束时的回调事件

代码：

    UPathFollowingComponent::OnMoveFinished

##### 如何获取两点之间的寻路路径(Vector数组)

代码：
    
    //4.20之前版本用法：UNavigationSystem* NavSys = UNavigationSystem::GetCurrent(GetWorld());
    UNavigationSystemV1* NavSys = UNavigationSystemV1::GetNavigationSystem(GetWorld());
     
    UNavigationPath *tpath = NavSys->FindPathToLocationSynchronously(GetWorld(), GetActorLocation(), end_point);
         
    if (tpath != NULL)
    {
         for (int pointiter = 0; pointiter < tpath->PathPoints.Num(); pointiter++)
         {
             DrawDebugSphere(GetWorld(), tpath->PathPoints[pointiter], 10.0f, 12, FColor(255, 0, 0));
         }
    }
	
##### Notice

Compilation Error:

	 error LNK2019: unresolved external symbol "__declspec(dllimport) public: static class UNavigationSystemV1 * __cdecl UNavigationSystemV1::GetNavigationSystem(class UObject *)" (__imp_?GetNavigationSystem@UNavigationSystemV1@@SAPEAV1@PEAVUObject@@@Z) referenced in function "protected: void __cdecl AMyPlayerController::SetNewMoveDestination(struct FVector)" (?SetNewMoveDestination@AMyPlayerController@@IEAAXUFVector@@@Z)
	1>SkillJoystickPlayerController.cpp.obj : error LNK2019: unresolved external symbol "__declspec(dllimport) public: static void __cdecl UNavigationSystemV1::SimpleMoveToLocation(class AController *,struct FVector const &)" (__imp_?SimpleMoveToLocation@UNavigationSystemV1@@SAXPEAVAController@@AEBUFVector@@@Z) referenced in function "protected: void __cdecl AMyPlayerController::SetNewMoveDestination(struct FVector)" (?SetNewMoveDestination@AMyPlayerController@@IEAAXUFVector@@@Z)
	
Solution:  
Add `NavigationSystem` into DependencyModule. e.g.:

	public class SkillJoystick : ModuleRules
	{
		public SkillJoystick(ReadOnlyTargetRules Target) : base(Target)
		{
			PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

			PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "NavigationSystem" });
		}
	}


参考：https://answers.unrealengine.com/questions/102126/how-do-i-get-the-navigation-path-to-a-point.html
    
