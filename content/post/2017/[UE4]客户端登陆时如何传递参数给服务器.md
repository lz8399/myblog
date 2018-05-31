---
title: "[UE4]客户端登陆时如何传递参数给服务器"
date: "2017-09-14T14:00:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Client、Dedicated Server、Passing Arguments、Login、ClientTravel

##### 客户端发送参数
执行PlayerController->ClientTravel时，默认Address URL如下：

    FString Address = TEXT("127.0.0.1:7777");

登陆时如果需要传递参数，则URL的格式如下：

    FString Address = FString::Printf(TEXT("127.0.0.1:7777?Param1=%s?Param2=%s"), *Param1, *Param2);

##### 服务端解析参数

先重写GameMode的InitNewPlayer()函数，然后再在该函数内做如下解析：

    FString AMyGameMode::InitNewPlayer(APlayerController* NewPlayerController, const FUniqueNetIdRepl& UniqueId, const FString& Options, const FString& Portal = TEXT(""))
    {
        FString Param1 = UGameplayStatics::ParseOption(Options, TEXT("Param1"));
        FString Param2 = UGameplayStatics::ParseOption(Options, TEXT("Param2"));
    }

官方文档：Passing Arguments To Server During Connection  
https://wiki.unrealengine.com/Passing_Arguments_To_Server_During_Connection

***
`明朝且做莫思量，如何过得今宵去？—周紫芝《踏莎行》`