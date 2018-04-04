+++
title= "[UE4][UE_LOG用法"
date= "2016-11-10T22:33:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

三种方式：

##### 方式1：GLog

    GLog->Log("Does something");
    
##### 方式2：UE_LOG(LogTemp)

    UE_LOG(LogTemp, Log, TEXT("%d"), 1111);
	UE_LOG(LogTemp, Warning, TEXT("%d"), 1111);
    
##### 方式3：自定义log

转载自：http://www.cnblogs.com/pengyingh/articles/5472998.html

头文件中加入：

    #pragma once

    #include "GameFramework/Actor.h"
    #include "FloatingActor.generated.h"
    DECLARE_LOG_CATEGORY_EXTERN(YourLog, Log, All);
    
cpp文件中加入：

    #include "FirstProject.h"
    #include "FloatingActor.h"

    DEFINE_LOG_CATEGORY(YourLog);

使用

    UE_LOG(YourLog, Warning, TEXT("Test UE_LOG %d"), rand());
    
##### 三种方式的输出结果

    Does something
    LogTemp: 1111
    LogTemp: Warning: 1111（黄色）
