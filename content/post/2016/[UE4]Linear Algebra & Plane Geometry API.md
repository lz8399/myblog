+++
title= "[UE4]Linear Algebra & Plane Geometry API"
date= "2016-06-23T23:35:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

keywords：UE4、Linear Algebra、Plane Geometry、线性代数、解析几何


##### 范围判定
    
检测一个点是否在一个多边形(或矩形)的内部(2D和3D)

    FBox2D::IsInside(const FVector2D& TestPoint)
    FBox::IsInside(const FVector& TestPoint)
    FIntRect::Contains( FIntPoint P )
    
##### 角度计算

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


##### 点坐标计算

计算直线外一点到该直线的最近的点（垂足的坐标）：
    
    FVector UKismetMathLibrary::FindClosestPointOnLine(FVector Point, FVector LineOrigin, FVector LineDirection);
    
计算直线与平面交叉点的坐标：
    
    bool UKismetMathLibrary::LinePlaneIntersection(const FVector& LineStart, const FVector& LineEnd, 
        const FPlane& APlane, float& T, FVector& Intersection);
        
计算平面外一点投射到平面的坐标点：
        
    FVector UKismetMathLibrary::ProjectPointOnToPlane(FVector Point, FVector PlaneBase, FVector PlaneNormal);

计算平面外矢量投射到平面后的矢量：
    
    FVector UKismetMathLibrary::ProjectVectorOnToPlane(FVector V, FVector PlaneNormal);

##### 插值相关

使用简单弹簧模型来 interpolate 浮点数值（范围从 Current 到 Target）

    float UKismetMathLibrary::FloatSpringInterp(float Current, float Target, UPARAM(ref) FFloatSpringState& SpringState, 
        float Stiffness, float CriticalDampingFactor, float DeltaTime, float Mass = 1.f);
        
同上，数值类型为 Vector：
        
    FVector UKismetMathLibrary::VectorSpringInterp(FVector Current, FVector Target, UPARAM(ref) FVectorSpringState& SpringState, float Stiffness, float CriticalDampingFactor, float DeltaTime, float Mass = 1.f);
        
Transform 插值计算：
        
    FTransform UKismetMathLibrary::TInterpTo(const FTransform& Current, const FTransform& Target, float DeltaTime, float InterpSpeed);
        
##### 向量相关

获取Rotator A 对应的3个方向向量：
    
    void UKismetMathLibrary::GetAxes(FRotator A, FVector& X, FVector& Y, FVector& Z);
    
获取 Rotator 对应坐标系3个方向向量：
    
    FVector UKismetMathLibrary::GetForwardVector(FRotator InRot);
	FVector UKismetMathLibrary::GetRightVector(FRotator InRot);
	FVector UKismetMathLibrary::GetUpVector(FRotator InRot);

计算一组向量的平均向量：
    
    FVector GetVectorArrayAverage(const TArray<FVector>& Vectors);