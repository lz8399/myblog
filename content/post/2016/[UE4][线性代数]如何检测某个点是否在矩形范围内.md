+++
title= "[UE4][线性代数]如何检测某个点是否在矩形范围内"
date= "2016-06-23T15:15:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API", "Math"]
+++

代码：

    FBox2D::IsInside(const FVector2D& TestPoint)
    FBox::IsInside(const FVector& TestPoint)
    FIntRect::Contains( FIntPoint P )