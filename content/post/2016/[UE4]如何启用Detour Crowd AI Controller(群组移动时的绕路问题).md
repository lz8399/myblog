+++
title= "[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)"
date= "2016-07-27T19:39:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

老版本中需要手动写C++来设置CrowManagerClass，新版本中只需要在Project Settings中设置。

##### 老版本

蓝图中叫做：`Detour Crowd AI Controller`
C++代码中叫做：`UCrowdFollowingComponent`，在AIController的构造函数中设置即可

头文件：

    MyAIController(const FObjectInitializer& ObjectInitializer = FObjectInitializer::Get());

cpp：

    MyAIController::MyAIController(const FObjectInitializer& ObjectInitializer)
        : Super(ObjectInitializer.SetDefaultSubobjectClass<UCrowdFollowingComponent>(TEXT("PathFollowingComponent")))
    {        
    }


##### 新版本
Project Settings -》Engine -》 Navigation System -》 Crow Manager Class

{{< figure src="/img/20160727-[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)/[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)-01.jpg">}}


官方doc：
FCrowdAvoidanceConfig
https://docs.unrealengine.com/latest/INT/API/Runtime/AIModule/Navigation/FCrowdAvoidanceConfig/index.html

注意事项：
使用UCrowdFollowingComponent时必须禁用RVO避让模式，否则无法生效：

    //默认是关闭的
    GetCharacterMovement()->bUseRVOAvoidance = false;	