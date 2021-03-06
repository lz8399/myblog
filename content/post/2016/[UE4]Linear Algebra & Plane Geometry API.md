+++
title= "[UE4]Linear Algebra & Plane Geometry API"
date= "2016-06-23T23:35:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

keywords：UE4、Linear Algebra、Plane Geometry、线性代数、解析几何

### 范围判定
    
检测一个点是否在一个多边形(或矩形)的内部(2D和3D)

    FBox2D::IsInside(const FVector2D& TestPoint)
    FBox::IsInside(const FVector& TestPoint)
    FIntRect::Contains( FIntPoint P )
    
### 角度计算

计算两个向量的夹角(Get an angle between 2 Vectors)，范围：(0, 180)

    float AimAtAngle = FMath::RadiansToDegrees(acosf(FVector::DotProduct(PlayerDirection, MouseDirection)));
    
参考：How to get an angle between 2 Vectors?  
https://answers.unrealengine.com/questions/31058/how-to-get-an-angle-between-2-vectors.html

        
计算方向向量与空间坐标轴（X、Y、Z）的夹角，范围：(-180, 180)

    FRotator Rot = UKismetMathLibrary::MakeRotFromX(TestVector);
    float Angle = Rot.Yaw;  //(-180, 180)
    
判断角色A在角色B的左边还是右边（或者角色A相对角色B的四个方向），参考自引擎代码：`UAnimInstance::CalculateDirection()`

    //-180到0表示 ActorA 在 ActorB 左边，0到180表示 ActorA 在 ActorB 右边
    float CalculateDirecton(const AActor* ActorA, const AActor* ActorB)
    {
        FVector TestDire = ActorA->GetActorLocation() - ActorB->GetActorLocation();

        FMatrix RotMatrix = FRotationMatrix(ActorB->GetActorRotation());
        FVector ForwardVector = RotMatrix.GetScaledAxis(EAxis::X);
        FVector RightVector = RotMatrix.GetScaledAxis(EAxis::Y);
        FVector NormalizedVel = TestDire.GetSafeNormal2D();

        // get a cos(alpha) of forward vector vs velocity
        float ForwardCosAngle = FVector::DotProduct(ForwardVector, NormalizedVel);
        // now get the alpha and convert to degree
        float ForwardDeltaDegree = FMath::RadiansToDegrees(FMath::Acos(ForwardCosAngle));

        // depending on where right vector is, flip it
        float RightCosAngle = FVector::DotProduct(RightVector, NormalizedVel);
        if (RightCosAngle < 0)
        {
            ForwardDeltaDegree *= -1;
        }
        
        return ForwardDeltaDegree;
    }

计算方向向量 InDirection 相对 ReferenceFrame 的方位俯仰角(Azimuth-Elevation)
    
    void UKismetMathLibrary::GetAzimuthAndElevation(FVector InDirection, const FTransform& ReferenceFrame, float& Azimuth, float& Elevation);
    
根据入射向量和法线向量计算反射向量

    FVector FMath::GetReflectionVector(const FVector& Direction, const FVector& SurfaceNormal);
    
根据地面的法线向量、Right方向向量、Up向量向量，计算出斜坡的 Roll 和 Pitch 方向的角度：
    
    void UKismetMathLibrary::GetSlopeDegreeAngles(const FVector& MyRightYAxis, const FVector& FloorNormal, const FVector& UpVector, 
        float& OutSlopePitchDegreeAngle, float& OutSlopeRollDegreeAngle);

		
### 点坐标计算

计算直线外一点到该直线的最近的点（垂足的坐标）：
    
    FVector UKismetMathLibrary::FindClosestPointOnLine(FVector Point, FVector LineOrigin, FVector LineDirection);
    
计算直线与平面交叉点的坐标：
    
    bool UKismetMathLibrary::LinePlaneIntersection(const FVector& LineStart, const FVector& LineEnd, 
        const FPlane& APlane, float& T, FVector& Intersection);
        
计算平面外一点投射到平面的坐标点：
        
    FVector UKismetMathLibrary::ProjectPointOnToPlane(FVector Point, FVector PlaneBase, FVector PlaneNormal);
	
### 向量（矢量）计算

向量A投射到以Z轴为法线的平面的投射向量

	/**
	 * Projects 2D components of vector based on Z.
	 *
	 * @return Projected version of vector based on Z.
	 */
	FVector Projection() const;

计算平面外矢量投射到平面后的矢量：
    
    FVector UKismetMathLibrary::ProjectVectorOnToPlane(FVector V, FVector PlaneNormal);
	
	static FVector VectorPlaneProject(const FVector& V, const FVector& PlaneNormal);
	

获取Rotator A 对应的3个方向向量：
    
    void UKismetMathLibrary::GetAxes(FRotator A, FVector& X, FVector& Y, FVector& Z);
    
获取 Rotator 对应坐标系3个方向向量：
    
    FVector UKismetMathLibrary::GetForwardVector(FRotator InRot);
	FVector UKismetMathLibrary::GetRightVector(FRotator InRot);
	FVector UKismetMathLibrary::GetUpVector(FRotator InRot);

计算一组向量的平均向量：
    
    FVector GetVectorArrayAverage(const TArray<FVector>& Vectors);
	
获取反向方向 / 获取A向量相对B向量的镜像向量

	/** 
	 * Given a direction vector and a surface normal, returns the vector reflected across the surface normal.
	 * Produces a result like shining a laser at a mirror!
	 *
	 * @param Direction Direction vector the ray is coming from.
	 * @param SurfaceNormal A normal of the surface the ray should be reflected on.
	 *
	 * @returns Reflected vector.
	 */
	static CORE_API FVector GetReflectionVector(const FVector& Direction, const FVector& SurfaceNormal);
	
以Rotator自身朝向为X轴，获取对应的Y、Z轴方向的世界坐标系方向

	FMatrix RotMatrix = FRotationMatrix(ActorB->GetActorRotation());
	FVector ForwardVector = RotMatrix.GetScaledAxis(EAxis::X);
	FVector RightVector = RotMatrix.GetScaledAxis(EAxis::Y);
	FVector TopVector = RotMatrix.GetScaledAxis(EAxis::Z);
	
Local space (Position, Direction or rotation) to world space:
	
	/** 
	 *	Transform a position by the supplied transform.
	 *	For example, if T was an object's transform, this would transform a position from local space to world space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform", meta=(Keywords="location"))
	static FVector UKismetMathLibrary::TransformLocation(const FTransform& T, FVector Location);

	/** 
	 *	Transform a direction vector by the supplied transform - will not change its length. 
	 *	For example, if T was an object's transform, this would transform a direction from local space to world space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform")
	static FVector UKismetMathLibrary::TransformDirection(const FTransform& T, FVector Direction);

	/** 
	 *	Transform a rotator by the supplied transform. 
	 *	For example, if T was an object's transform, this would transform a rotation from local space to world space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform")
	static FRotator UKismetMathLibrary::TransformRotation(const FTransform& T, FRotator Rotation);
	
World space (Position, Direction or rotation) to local space:

	/** 
	 *	Transform a position by the inverse of the supplied transform.
	 *	For example, if T was an object's transform, this would transform a position from world space to local space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform", meta=(Keywords="location"))
	static FVector UKismetMathLibrary::InverseTransformLocation(const FTransform& T, FVector Location);

	/** 
	 *	Transform a direction vector by the inverse of the supplied transform - will not change its length.
	 *	For example, if T was an object's transform, this would transform a direction from world space to local space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform")
	static FVector UKismetMathLibrary::InverseTransformDirection(const FTransform& T, FVector Direction);

	/** 
	 *	Transform a rotator by the inverse of the supplied transform. 
	 *	For example, if T was an object's transform, this would transform a rotation from world space to local space.
	 */
	UFUNCTION(BlueprintPure, Category="Math|Transform")
	static FRotator UKismetMathLibrary::InverseTransformRotation(const FTransform& T, FRotator Rotation);

### 插值相关

使用简单弹簧模型来 interpolate 浮点数值（范围从 Current 到 Target）

    float UKismetMathLibrary::FloatSpringInterp(float Current, float Target, UPARAM(ref) FFloatSpringState& SpringState, 
        float Stiffness, float CriticalDampingFactor, float DeltaTime, float Mass = 1.f);
        
同上，数值类型为 Vector：
        
    FVector UKismetMathLibrary::VectorSpringInterp(FVector Current, FVector Target, UPARAM(ref) FVectorSpringState& SpringState, float Stiffness, float CriticalDampingFactor, float DeltaTime, float Mass = 1.f);
        
Transform 插值计算：
        
    FTransform UKismetMathLibrary::TInterpTo(const FTransform& Current, const FTransform& Target, float DeltaTime, float InterpSpeed);
	
### 坐标系相关

##### Rotation变换
世界坐标系转局部（本地）坐标系（World To Local）：

	FORCEINLINE FQuat FTransform::InverseTransformRotation(const FQuat& Q) const;
	
示例代码：

	FRotator DestWorldRot(100.f, 100.f, 0.f);
	FQuat QuatWorld = DestWorldRot.Quaternion();
	FQuat QuatLocal = MyActor->GetComponentTransform().InverseTransformRotation(QuatWorld);
	FRotator RotOffset = QuatLocal.Rotator();
        
局部（本地）坐标系转世界坐标系（Local To World）：

	FORCEINLINE FQuat FTransform::TransformRotation(const FQuat& Q) const;
	
示例代码：

	FRotator DestRotOffset(100.f, 100.f, 0.f);
	FRotator DestWorldRot = FTransform(CameraRotOrig).TransformRotation(DestRotOffset.Quaternion()).Rotator();
	
##### Location变换

World To Local:

	FORCEINLINE FVector FTransform::InverseTransformPositionNoScale(const FVector &V) const;
	
Local To World:

	FORCEINLINE FVector FTransform::TransformPositionNoScale(const FVector& V) const;
	
##### Direction变换

World To Local:

	FORCEINLINE FVector FTransform::InverseTransformVectorNoScale(const FVector &V) const
	
示例代码：

	//返回摄像机Rotation相对角色Rotation的偏移量Offset
	FRotator ASBaseCharacter::GetAimOffsets() const
	{
		const FVector AimDirWS = GetBaseAimRotation().Vector();
		const FVector AimDirLS = ActorToWorld().InverseTransformVectorNoScale(AimDirWS);
		const FRotator AimRotLS = AimDirLS.Rotation();

		return AimRotLS;
	}
	
代码出处：  
https://github.com/tomlooman/EpicSurvivalGameSeries/blob/4a6ee9a6081529fadbe0f693b2e4e6729d5ec08d/SurvivalGame/Source/SurvivalGame/Private/Player/SBaseCharacter.cpp#L374
	
Local To World:
	
	FORCEINLINE FVector FTransform::TransformVectorNoScale(const FVector& V) const
	
{{< alert warning >}}
如果想获取两个Rotation之间的Offset，更简单的办法是做相减：`FRotator Offset = R2 - R1;`。但这种直接相减的方式，返回的结果Rotation，度数可能会小于-180 或 大于 180，需要手动处理范围限定，但是效率远高于`InverseTransformVector`
{{< /alert >}}
	
### 曲线相关

贝塞尔曲线

	/**
	 * Generates a list of sample points on a Bezier curve defined by 2 points.
	 *
	 * @param ControlPoints	Array of 4 FVectors (vert1, controlpoint1, controlpoint2, vert2).
	 * @param NumPoints Number of samples.
	 * @param OutPoints Receives the output samples.
	 * @return The path length.
	 */
	static CORE_API float FVector::EvaluateBezier(const FVector* ControlPoints, int32 NumPoints, TArray<FVector>& OutPoints);
	
`无欲则刚，关心则乱。----《论语》`