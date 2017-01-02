+++
title= "[UE4]CharacterMoveComponent中各个属性的意义及默认值"
date= "2016-06-22T16:10:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

AirControl: 当Jumping或者Falling的时候，侧向移动的速度。默认为0.05，1表示以最大速度侧向移动，0表示禁止侧向移动

    CharacterMovement	0x000002244572a400 (Name=0x0000022474e0aab8 "CharMoveComp")	UCharacterMovementComponent * {UE4Editor-Engine.dll!UCharacterMovementComponent}

    [UCharacterMovementComponent]	(Name=0x0000022474e0aab8 "CharMoveComp")	UE4Editor-Engine.dll!UCharacterMovementComponent
    UPawnMovementComponent	(Name=0x0000022474e0aab8 "CharMoveComp")	UPawnMovementComponent
    IRVOAvoidanceInterface	{...}	IRVOAvoidanceInterface
    INetworkPredictionInterface	{...}	INetworkPredictionInterface
    CharacterOwner	0x000002244571ab00 (Name=0x000002240ef84228 "pawn_shuangtouguai_charBP_C"_0)	ACharacter * {AWarriorCharacter}
    GravityScale	1.00000000	float
    MaxStepHeight	45.0000000	float
    JumpZVelocity	420.000000	float
    JumpOffJumpZFactor	0.500000000	float
    WalkableFloorAngle	44.7650833	float
    WalkableFloorZ	0.710000038	float
    MovementMode	MOVE_None (0)	TEnumAsByte<enum EMovementMode>
    CustomMovementMode	0 '\0'	unsigned char
    OldBaseLocation	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    OldBaseQuat	{X=0.000000000 Y=0.000000000 Z=0.000000000 ...}	FQuat
    GroundFriction	8.00000000	float
    MaxWalkSpeed	600.000000	float
    MaxWalkSpeedCrouched	300.000000	float
    MaxSwimSpeed	300.000000	float
    MaxFlySpeed	600.000000	float
    MaxCustomMovementSpeed	600.000000	float
    MaxAcceleration	2048.00000	float
    BrakingFrictionFactor	2.00000000	float
    BrakingFriction	0.000000000	float
    bUseSeparateBrakingFriction	0	unsigned int
    BrakingDecelerationWalking	2048.00000	float
    BrakingDecelerationFalling	0.000000000	float
    BrakingDecelerationSwimming	0.000000000	float
    BrakingDecelerationFlying	0.000000000	float
    AirControl	0.0500000007	float
    AirControlBoostMultiplier	2.00000000	float
    AirControlBoostVelocityThreshold	25.0000000	float
    FallingLateralFriction	0.000000000	float
    CrouchedHalfHeight	40.0000000	float
    Buoyancy	1.00000000	float
    PerchRadiusThreshold	0.000000000	float
    PerchAdditionalHeight	40.0000000	float
    RotationRate	{Pitch=0.000000000 Yaw=640.000000 Roll=0.000000000 }	FRotator
    bUseControllerDesiredRotation	0	unsigned int
    bOrientRotationToMovement	1	unsigned int
    bMovementInProgress	0	unsigned int
    bEnableScopedMovementUpdates	1	unsigned int
    bForceMaxAccel	0	unsigned int
    bRunPhysicsWithNoController	0	unsigned int
    bForceNextFloorCheck	1	unsigned int
    bShrinkProxyCapsule	1	unsigned int
    bCanWalkOffLedges	1	unsigned int
    bCanWalkOffLedgesWhenCrouching	0	unsigned int
    bNetworkSmoothingComplete	1	unsigned int
    bDeferUpdateMoveComponent	0	unsigned int
    DeferredUpdatedMoveComponent	0x0000000000000000 <NULL>	USceneComponent *
    MaxOutOfWaterStepHeight	40.0000000	float
    OutofWaterZ	420.000000	float
    Mass	100.000000	float
    bEnablePhysicsInteraction	true	bool
    bTouchForceScaledToMass	true	bool
    bPushForceScaledToMass	false	bool
    bPushForceUsingZOffset	false	bool
    bScalePushForceToVelocity	true	bool
    StandingDownwardForceScale	1.00000000	float
    InitialPushForceFactor	500.000000	float
    PushForceFactor	750000.000	float
    PushForcePointZOffsetFactor	-0.750000000	float
    TouchForceFactor	1.00000000	float
    MinTouchForce	-1.00000000	float
    MaxTouchForce	250.000000	float
    RepulsionForce	2.50000000	float
    bForceBraking_DEPRECATED	0	unsigned int
    CrouchedSpeedMultiplier_DEPRECATED	0.500000000	float
    UpperImpactNormalScale_DEPRECATED	0.500000000	float
    Acceleration	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    LastUpdateLocation	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    LastUpdateRotation	{X=0.000000000 Y=0.000000000 Z=0.000000000 ...}	FQuat
    LastUpdateVelocity	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    ServerLastTransformUpdateTimeStamp	0.000000000	float
    PendingImpulseToApply	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    PendingForceToApply	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    AnalogInputModifier	0.000000000	float
    MaxSimulationTimeStep	0.0500000007	float
    MaxSimulationIterations	8	int
    NetworkSimulatedSmoothLocationTime	0.100000001	float
    NetworkSimulatedSmoothRotationTime	0.0329999998	float
    ListenServerNetworkSimulatedSmoothLocationTime	0.0399999991	float
    ListenServerNetworkSimulatedSmoothRotationTime	0.0329999998	float
    NetworkMaxSmoothUpdateDistance	256.000000	float
    NetworkNoSmoothUpdateDistance	384.000000	float
    NetworkSmoothingMode	Exponential (2 '\x2')	ENetworkSmoothingMode
    LedgeCheckThreshold	4.00000000	float
    JumpOutOfWaterPitch	11.2500000	float
    CurrentFloor	{bBlockingHit=0 bWalkableFloor=0 bLineTrace=0 ...}	FFindFloorResult
    DefaultLandMovementMode	MOVE_Walking (1)	TEnumAsByte<enum EMovementMode>
    DefaultWaterMovementMode	MOVE_Swimming (4)	TEnumAsByte<enum EMovementMode>
    GroundMovementMode	MOVE_Walking (1)	TEnumAsByte<enum EMovementMode>
    bMaintainHorizontalGroundVelocity	1	unsigned int
    bImpartBaseVelocityX	1	unsigned int
    bImpartBaseVelocityY	1	unsigned int
    bImpartBaseVelocityZ	1	unsigned int
    bImpartBaseAngularVelocity	1	unsigned int
    bJustTeleported	1	unsigned int
    bNetworkUpdateReceived	0	unsigned int
    bNetworkMovementModeChanged	0	unsigned int
    bIgnoreClientMovementErrorChecksAndCorrection	0	unsigned int
    bNotifyApex	0	unsigned int
    bCheatFlying	0	unsigned int
    bWantsToCrouch	0	unsigned int
    bCrouchMaintainsBaseLocation	0	unsigned int
    bIgnoreBaseRotation	0	unsigned int
    bFastAttachedMove	0	unsigned int
    bAlwaysCheckFloor	1	unsigned int
    bUseFlatBaseForFloorChecks	0	unsigned int
    bPerformingJumpOff	0	unsigned int
    bWantsToLeaveNavWalking	0	unsigned int
    bUseRVOAvoidance	0	unsigned int
    bRequestedMoveUseAcceleration	1	unsigned int
    bHasRequestedVelocity	0	unsigned int
    bRequestedMoveWithMaxSpeed	0	unsigned int
    bWasAvoidanceUpdated	0	unsigned int
    bUseRVOPostProcess	0	unsigned int
    bDeferUpdateBasedMovement	0	unsigned int
    bProjectNavMeshWalking	0	unsigned int
    bProjectNavMeshOnBothWorldChannels	0	unsigned int
    AvoidanceLockVelocity	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    AvoidanceLockTimer	0.000000000	float
    AvoidanceConsiderationRadius	500.000000	float
    RequestedVelocity	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    AvoidanceUID	0	int
    AvoidanceGroup	{bGroup0=1 bGroup1=0 bGroup2=0 ...}	FNavAvoidanceMask
    GroupsToAvoid	{bGroup0=1 bGroup1=1 bGroup2=1 ...}	FNavAvoidanceMask
    GroupsToIgnore	{bGroup0=0 bGroup1=0 bGroup2=0 ...}	FNavAvoidanceMask
    AvoidanceWeight	0.000000000	float
    PendingLaunchVelocity	{X=0.000000000 Y=0.000000000 Z=0.000000000 }	FVector
    CachedNavLocation	{Location={X=0.000000000 Y=0.000000000 Z=0.000000000 } NodeRef=0 }	FNavLocation
    CachedProjectedNavMeshHitResult	{bBlockingHit=0 bStartPenetrating=0 Time=1.00000000 ...}	FHitResult
    NavMeshProjectionInterval	0.100000001	float
    NavMeshProjectionTimer	0.000000000	float
    NavMeshProjectionInterpSpeed	12.0000000	float
    NavMeshProjectionHeightScaleUp	0.670000017	float
    NavMeshProjectionHeightScaleDown	1.00000000	float
    PostPhysicsTickFunction	{Target=0x000002244572a400 (Name=0x0000022474e0aab8 "CharMoveComp") }	FCharacterMovementComponentPostPhysicsTickFunction
    ClientPredictionData	0x0000000000000000 <NULL>	FNetworkPredictionData_Client_Character *
    ServerPredictionData	0x0000000000000000 <NULL>	FNetworkPredictionData_Server_Character *
    MinTimeBetweenTimeStampResets	240.000000	float
    CurrentRootMotion	{RootMotionSources=Empty PendingAddRootMotionSources=Empty bHasAdditiveSources=false ...}	FRootMotionSourceGroup
    RootMotionIDMappings	Empty	TArray<FRootMotionServerToLocalIDMapping,TInlineAllocator<16,FDefaultAllocator> >
    RootMotionParams	{bHasRootMotion=false BlendWeight=0.000000000 RootMotionTransform={Rotation={m128_f32=0x000002244572aa80 {...} ...} ...} }	FRootMotionMovementParams
    bWasSimulatingRootMotion	false	bool