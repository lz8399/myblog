---
title: "[UE4]获取系统时间以及UNIX时间戳"
date: "2016-08-06T22:59:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

蓝图：

    float UKismetSystemLibrary::GetGameTimeInSeconds(UObject* WorldContextObject);
    
C++代码：

    double now = FPlatformTime::Seconds();