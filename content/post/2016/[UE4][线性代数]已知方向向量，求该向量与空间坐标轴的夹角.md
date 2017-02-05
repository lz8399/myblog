+++
title= "[UE4][线性代数]已知方向向量，求该向量与空间坐标轴的夹角"
date= "2016-07-06T17:30:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API", "Math"]
+++


原始的数学公式不列举了，需要的话找个Math库看下源码。这里以UE4的API说明：

情况一：
已知空间中两个点FVector V1, V2，方向向量V3 = V2 - V1，求V3与空间坐标的夹角：

    FRotator R = (V2 - V1).Rotation();

情况二：
已知方向向量Vector V1，求V1与空间坐标轴的夹角Rotator R1：即将Vector转换为Rotator

    FRotator R1 = FVector(100.f, 100.f, 0.f).Rotation();
    FRotator R2 = FVector(-100.f, -100.f, 0.f).Rotation();
    FRotator R3 = FVector(100.f, 0.f, 0.f).Rotation();
    FRotator R4 = FVector(0.f, 100.f, 0.f).Rotation();

结果分别是：

    R1 = {Pitch=0.0 Yaw=45.0 Roll=0.0 }
    R2 = {Pitch=0.0 Yaw=-135.0 Roll=0.0 }
    R3 = {Pitch=0.0 Yaw=0.0 Roll=0.0 }
    R4 = {Pitch=0.0 Yaw=90.0 Roll=0.0 }


FVector::Rotation()函数的内部实现（局部）：

    FRotator R;

    // Find yaw.
    R.Yaw = FMath::Atan2(Y,X) * (180.f / PI);

    // Find pitch.
    R.Pitch = FMath::Atan2(Z,FMath::Sqrt(X*X+Y*Y)) * (180.f / PI);

    // Find roll.
    R.Roll = 0;

    return R;