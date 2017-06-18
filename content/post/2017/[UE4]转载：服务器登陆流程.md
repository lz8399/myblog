---
title: "[UE4]转载：服务器登陆流程"
date: "2017-06-01T13:00:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

原文：http://blog.csdn.net/xiaozhi0999/article/details/51393704


ue4中，客户端登陆流程如下，调用UEngine::Browse方法，在这个方法中，判断如果是客户端，则创建UPendingNetGame实例，代码如下：

    WorldContext.PendingNetGame = NewObject<UPendingNetGame>();  
    WorldContext.PendingNetGame->Initialize(URL);  
    WorldContext.PendingNetGame->InitNetDriver();  
    
而在InitNetDriver函数中，会向服务器发送 NMT_Hello 协议，我们转到NMT_Hello 的定义，如下：

    DEFINE_CONTROL_CHANNEL_MESSAGE_TWOPARAM(Hello, 0, uint8, uint32); // initial client connection message  

参数1：大端还是小端  
参数2：客户端版本号

客户端处理协议的地方是如下两个函数：

    void UPendingNetGame::NotifyControlMessage(UNetConnection* Connection, uint8 MessageType, class FInBunch& Bunch)  
    void UWorld::NotifyControlMessage(UNetConnection* Connection, uint8 MessageType, class FInBunch& Bunch)  
    
服务器处理协议的地方是下面这个函数：

    void UWorld::NotifyControlMessage(UNetConnection* Connection, uint8 MessageType, class FInBunch& Bunch)  

在服务器的协议处理函数，我们可以看到NMT_Hello协议的处理过程，先调用Receive接收消息，然后判断版本号是否一致，不一致发送NMT_Upgrade消息，一致则发送NMT_Challenge消息

    DEFINE_CONTROL_CHANNEL_MESSAGE_ONEPARAM(Challenge, 3, FString); // server sends client challenge string to verify integrity  
    
客户端收到NMT_Challenge消息后，向服务器发送NMT_Login消息，NMT_Login消息携带三个参数，如下：

    DEFINE_CONTROL_CHANNEL_MESSAGE_THREEPARAM(Login, 5, FString, FString, FUniqueNetIdRepl); // client requests to be admitted to the game  

参数1：客户端响应  
参数2：客户端URL  
参数3：客户端唯一ID  
服务器收到NMT_Login消息，验证是否可以登录，失败返回NMT_Failure消息，成功则向服务器发送NMT_Welcome消息

NMT_Welcome消息定义如下: 

    DEFINE_CONTROL_CHANNEL_MESSAGE_THREEPARAM(Welcome, 1, FString, FString, FString); // server tells client they're ok'ed to load the server's level  

参数1：服务器使用地图名  
参数2：服务器使用GameMode名称  
参数3：重定向URL  

客户端收到NMT_Welcome消息，向服务器发送NMT_Netspeed消息，定义如下：

    DEFINE_CONTROL_CHANNEL_MESSAGE_ONEPARAM(Netspeed, 4, int32); // client sends requested transfer rate  

参数1：当前网络传输速度  
服务器收到NMT_Netspeed消息，只是简单记录一下客户端的NetSpeed即可

这里有个问题先要说明一下，客户端何时加载地图？

在下面这个函数中：

    void UEngine::TickWorldTravel(FWorldContext& Context, float DeltaSeconds)  

有如下这个判断：

    else if( Context.PendingNetGame && Context.PendingNetGame->bSuccessfullyConnected && !Context.PendingNetGame->bSentJoinRequest )  

当bSuccessfullyConnected为true而bSentJoinRequest为false时，客户端会LoadMap，而bSuccessfullyConnected是在客户端处理完NMT_Welcome消息后设置为true的，也就是说客户端在处理完NMT_Welcome消息，下一次执行TickWorldTravel函数的时候，就会加载地图，而bSentJoinRequest变量，是为了防止地图被加载多次而设置的。

当客户端调用完LoadMap，会向服务器发送NMT_Join消息，在服务器处理NMT_Join消息时，代码如下：

    Connection->PlayerController = SpawnPlayActor( Connection, ROLE_AutonomousProxy, InURL, Connection->PlayerId, ErrorMsg );  
        
然后SpawnPlayActor中会调用GameMode的Login，而在Login内部，会调用如下代码，创建PlayerController

    APlayerController* NewPlayerController = SpawnPlayerController(RemoteRole, FVector::ZeroVector, FRotator::ZeroRotator);  

在PlayerController的初始化函数中，如果是服务器，则创建PlayerState，用于服务器和客户端Player信息的同步，具体函数如下：

    void APlayerController::PostInitializeComponents()  


    
