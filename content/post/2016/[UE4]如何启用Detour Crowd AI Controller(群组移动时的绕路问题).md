+++
title= "[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)"
date= "2016-07-27T19:39:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

keywords：UE4、AI、群体移动、闪避、避让、回避

##### Detour Crowd AI Controller

蓝图方式  
打开ControllerBP，在 `Class Settings` 中设置 `Parent Class` 为：`Detour Crowd AI Controller`。  


C++方式  

引擎的C++代码有个叫 `ADetourCrowdAIController` 的class，但是这个class无法继承；  
要在C++中使用Detour Crowd AI，需要借助 `UCrowdFollowingComponent`，在AIController的构造函数中设置即可

头文件：

    MyAIController(const FObjectInitializer& ObjectInitializer = FObjectInitializer::Get());

cpp：

    MyAIController::MyAIController(const FObjectInitializer& ObjectInitializer)
        : Super(ObjectInitializer.SetDefaultSubobjectClass<UCrowdFollowingComponent>(TEXT("PathFollowingComponent")))
    {        
    }


##### Crowd Manager 配置
Project Settings -》Engine -》 Navigation System -》 Crowd Manager Class

{{< figure src="/img/20160727-[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)/[UE4]如何启用Detour Crowd AI Controller(群组移动时的绕路问题)-01.jpg">}}

并可以在 Project Settings -》 Engine -》 Crowd Manager 编辑各种参数。

官方doc：
FCrowdAvoidanceConfig
https://docs.unrealengine.com/latest/INT/API/Runtime/AIModule/Navigation/FCrowdAvoidanceConfig/index.html

##### 注意事项

1，使用UCrowdFollowingComponent时必须禁用RVO避让模式，否则无法生效：

    //默认是关闭的
    GetCharacterMovement()->bUseRVOAvoidance = false;	
    
2，自定义 `CrowdManager` 无法生效的bug  
4.18有这个问题，最新版是否修复本没测过。

现象：  
新建的自定义 `CrowdManager`，即使在设置中（Project Settings -》Engine -》 Navigation System -》 Crowd Manager Class）设置了，也不会起效。

原因：  
UE4的bug。

解决办法：

+ 1. 继承NavigationSystem。
+ 2. 复写NavigationSystem::CreateCrowdManager()
直接在函式内生成你的CrowdManager并传进SetCrowdManager：
SetCrowdManager(NewObject<UCrowdManagerBase>(this, UMyCrowdManager::StaticClass())); 
+ 3. 到Engine/Config/DefaultEngine. ini加下面两行
[/Script/Engine.Engine] 
NavigationSystemClassName=/Script/[YourProjectName].[NavigationClassName] 
+ 4.关掉Editor重开，就可以试试看你的CrowdManager是不是运作了~

3，移动时转向抖动的问题  
现象：  
启用 `UCrowdFollowingComponent` 之后，角色群体移动时，转向时经常抖动（朝向瞬切）。

原因：  
可能是每帧都在执行移动，且使用的API为：`UNavigationSystem::SimpleMoveToLocation()`。

解决办法：  
如果要使用 `UNavigationSystem::SimpleMoveToLocation()`，就不要每帧执行，可以间隔几秒执行一次。  
如果使用 `AAIController::MoveToLocation()`，则没这个问题，即使每帧执行，也不会抖动。

4，群体移动时，一部分移动，一部分静止不动  
解决办法：  
将 `Max Agents` 改大一点。（Project Settings -> Engine -> Crowd Manager -> Max Agents）

##### 参考资料
Crowd Manager Avoidance Config（推荐）  
https://answers.unrealengine.com/questions/212408/crowd-manager-avoidance-config.html

Unreal Avoidance系统(上)  
https://yekdniwunrealengine.blogspot.com/2018/02/unreal-avoidance_10.html

Unreal Avoidance系统(下)  
https://yekdniwunrealengine.blogspot.com/2018/02/unreal-avoidance.html