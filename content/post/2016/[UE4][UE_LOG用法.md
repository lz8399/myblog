+++
title= "[UE4][UE_LOG用法"
date= "2016-11-10T22:33:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

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
