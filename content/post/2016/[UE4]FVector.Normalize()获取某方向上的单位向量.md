---
title: "[UE4]FVector.Normalize()获取某方向上的单位向量"
date: "2016-09-06T21:49:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keyworlds：**单位向量、方向向量、unit vector**

FVector::Normalize()函数的意思是将当前向量变成单位向量（方向与原向量相同，但是长度为1）。

使用场景：
1，	比如你需要做一些平滑计算的时候，那么可能会用到DeltaSeconds，你想包装你的向量与DeltaSeconds运算时始终保持恒定，那么，可以将该向量Normalize。
2，	想获得两个点之间的单位向量，一边把该单位向量当作MovementComponent的速率。


与之对应的两种蓝图方式：

1，Get Direction Vector
{{< figure src="/img/20160906-[UE4]FVector.Normalize()获取某方向上的单位向量.jpg">}}  

2，与C++函数名同名的`Normalize`节点
