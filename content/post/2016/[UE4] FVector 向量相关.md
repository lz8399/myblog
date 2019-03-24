---
title: "[UE4] FVector 向量相关"
date: "2016-09-06T21:49:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keywords：单位向量、方向向量、unit vector

##### 获取某方向上的单位向量

使用场景：

1. 	比如你需要做一些平滑计算的时候，那么可能会用到DeltaSeconds，该向量与DeltaSeconds运算时，希望该向量始终保持恒定，那么，可以将该向量Normalize。
2. 想获得两个点之间的单位向量，一般把该单位向量当作 MovementComponent 的方向。


与之对应的两种蓝图方式：

1，Get Direction Vector
{{< figure src="/img/20160906-[UE4] FVector 向量相关/[UE4] FVector 向量相关-01.jpg">}}  

2，Normalize
{{< figure src="/img/20160906-[UE4] FVector 向量相关/[UE4] FVector 向量相关-02.jpg">}}
{{< alert danger >}}
C++ 方式：蓝图节点 `Normalize` 对应的 C++ 接口是 `FVector::GetSafeNormal()`，而不是`FVector::Normalize()`。前者是返回一个单位向量，但不会修改当前向量；后者不返回任何值，但是会修改当前向量为单位向量。
{{< /alert >}}

##### FVector::Rotation()对应的蓝图节点

    void GetYawPitchFromVector(FVector InVec, float& Yaw, float& Pitch);

{{< figure src="/img/20160906-[UE4] FVector 向量相关/[UE4] FVector 向量相关-03.jpg">}}  

然后使用输出参数 Yaw, Pitch 创建一个 Rotator，并将 Roll 设置为0，即等价于`FVector::Rotation()`。

