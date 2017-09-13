---
title: "[UE4]No owning connection for actor XXX. Function XXX will not be processed"
date: "2017-09-12T18:26:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Dedicated Server、Replication、独立服务器

在客户端连接独立服务端的情况下，客户端执行Server函数时提示以下警告：

    LogNet: Warning: UIpNetDriver::ProcesRemoteFunction: No owning connection for actor TopDownCharacter_C_0. Function ServerMoveToDest will not be processed.
    
原因：  
Client执行Server函数的对象，是在服务端Spawn出来的，不是在客户端创建的，所以提示这个警告。  
比如你在Server端的GameMode中创建了一个Character，且这个Character的Replicated相关属性设置为true，你在客户端用这个Character对象来执行Server函数（即UFUNCTION(Server, Reliable)函数），这时就会提示这个错误。  
UE4独立服务端的规则时，只有在客户端创建的对象才有允许执行Server函数，比如PlayerController，这个是引擎自动在客户端创建的对象，它身上的Server函数可以在客户端调用且在服务端执行。

解决办法：  
如果你的逻辑是要操作某个服务端创建的对象，比如刚刚说的在服务端Spawn出来的Character，可以先通过PlayerController执行Server函数，在其Server函数内部获取服务端的Character对象，然后再执行相关逻辑。

UE4独立服务器的几个注意要点：  

+ Replicated属性只允许服务端修改，而不允许客户端修改。
+ 客户端和客户端之间无法直接通信，只能通过独立服务器广播通知。
+ 客户端要执行服务端函数，则执行对象必须是在客户端Spawn出来的，服务端创建的且复制到客户端的对象，没有权限执行服务端函数。这也很好理解，这是为了保证安全性。