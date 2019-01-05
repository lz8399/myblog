---
title: "[UE4][线性代数]基于某点向某方向上投射指定距离后的坐标计算"
date: "2016-07-06T19:54:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Math
---

代码：

    float Len = FMath::Sqrt(100 * 100 + 100 * 100);
    FVector Loc = FVector(100.f, 100.f, 0.f) + FRotator(0.f, 45.f, 0.f).Vector() * Len;

结果：

    Loc = {X=200.f, Y=200.f, Z=0.f}
	
{{< alert info >}}
`FRotator::Vector()`对应的蓝图函数为`GetRotationXVector`
{{< /alert >}}

=================================

例子2：

    float Len = FMath::Sqrt(100 * 100 + 100 * 100);
    FVector Loc1 = FVector(0.f, 0.f, 0.f) + FRotator(0.f, 45.f, 0.f).Vector() * Len;
    FVector Loc2 = FVector(0.f, 0.f, 0.f) + FRotator(0.f, 135.f, 0.f).Vector() * Len;
    FVector Loc3 = FVector(0.f, 0.f, 0.f) + FRotator(0.f, 225.f, 0.f).Vector() * Len;
    FVector Loc4 = FVector(0.f, 0.f, 0.f) + FRotator(0.f, 315.f, 0.f).Vector() * Len;

结果：

    Loc1 = {X=100.f, Y=100.f, Z=0.f}
    Loc2 = {X=-100.f, Y=100.f, Z=0.f}
    Loc3 = {X=-100.f, Y=-100.f, Z=0.f}
    Loc4 = {X=100.f, Y=-100.f, Z=0.f}