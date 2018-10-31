---
title: "[UE4]Time时间相关"
date: "2016-08-06T22:59:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

##### 获取系统时间以及UNIX时间戳

蓝图：

    float UKismetSystemLibrary::GetGameTimeInSeconds(UObject* WorldContextObject);
    
C++代码：

    FDateTime Time = FDateTime::Now();
    int64 Timestamp = Time.ToUnixTimestamp();
    
##### 将 Unix Timestamp 转换为年月日（year, month, day）

    FDateTime Time = FDateTime::FromUnixTimestamp(int64 UnixTime);
    

##### 获取系统当前日期时间：年月日时分秒

    FDateTime Time = FDateTime::Now();

    int Year = Time.GetYear();
    int Month = Time.GetMonth();
    int Day = Time.GetDay();
    
    int Hour = Time.GetHour();
	int Minute = Time.GetMinute();
	int Second = Time.GetSecond();
    
##### 获取CPU时钟周期
    
    //微妙格式
    uint64 cycle = FPlatformTime::Cycles64();
    uint32 cycle = FPlatformTime::Cycles();
    
    //秒格式
    double now = FPlatformTime::Seconds();