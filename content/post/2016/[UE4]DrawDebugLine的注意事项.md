---
title: "[UE4]DrawDebugLine的注意事项"
date: "2016-10-07T01:05:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

有时候调用DrawDebugLine划线，在场景中看不见：

    DrawDebugLine(GameMode->GetWorld(), StartLocation, EndLocation, FColor::Red);

代码上没有任何问题，如果还是看不见，则可能是天光太强，导致线条没有渲染出来。

##### 解决办法：
按F2关掉天光，或者按F1开启mesh透视模式