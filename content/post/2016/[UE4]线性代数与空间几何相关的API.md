+++
title= "[UE4]线性代数与空间几何相关的API"
date= "2016-06-23T23:35:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++


检测一个点是否在一个多边形(或矩形)的内部(2D和3D)

    FBox2D::IsInside(const FVector2D& TestPoint)
    FBox::IsInside(const FVector& TestPoint)
    FIntRect::Contains( FIntPoint P )