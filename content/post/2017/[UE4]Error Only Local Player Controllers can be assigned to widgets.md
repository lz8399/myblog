---
title: "[UE4]Error Only Local Player Controllers can be assigned to widgets"
date: "2017-09-14T19:39:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---


服务端错误提示：

    PIE: Error: Only Local Player Controllers can be assigned to widgets. MyPlayerController_0 is not a Local Player Controller.
    
原因：  
在服务端创建客户端相关的对象时，则会报这个错误，比如创建一个Widget，需要判断下是客户端还是服务端。

解决办法：  
在创建Widget时判断下是否为服务器，例如：

    void AReplTestPlayerController::BeginPlay()
    {
        if (GetNetMode() == NM_Standalone)
        {
            if (UClass* BPClass = LoadClass<UMyUserWidget>(NULL, TEXT("WidgetBlueprint'/Game/TopDownCPP/Blueprints/NewWidgetBlueprint.NewWidgetBlueprint_C'")))
            {
                LoginWidget = CreateWidget<UMyUserWidget>(this, BPClass);
                if (LoginWidget)
                {
                    LoginWidget->AddToViewport();
                }
            }
        }
    }