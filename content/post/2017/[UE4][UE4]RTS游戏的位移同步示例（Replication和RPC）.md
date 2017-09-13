+++
title= "[UE4]RTS游戏的位移同步示例（Replication和RPC）"
date= "2017-02-25T20:33:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
draft = true
+++


keywords：UE4、Replication、Relicate、reliable、RPC、RTS Movement、Dedicated Server、属性同步、demo、example

##### 属性同步
步骤：  
1，对属性添加UPROPERTY(Replicated)宏：

    //Player unique ID
	UPROPERTY(Replicated)
		int PlayerSerial_;

2，属性所在的class中重写函数GetLifetimeReplicatedProps：  
需要头文件：

    #include "Net/UnrealNetwork.h"
    
重写函数：

    void AReplTestCharacter::GetLifetimeReplicatedProps(TArray< FLifetimeProperty > & OutLifetimeProps) const
    {
        Super::GetLifetimeReplicatedProps(OutLifetimeProps);

        DOREPLIFETIME(AReplTestCharacter, PlayerSerial_);
    }
    
##### RPC（远程执行调用）
步骤：  
1，对需要远程执行的函数添加宏UFUNCTION(Server, Reliable, WithValidation)或者UFUNCTION(Client, Reliable)。其中Server表示在客户端调用，在服务端执行，Client则反之；WithValidation表示是否需要验证函数，加上的画需要添加函数：bool MyFun_Validate()，函数提内容写在MyFun_Implementation函数内。cpp中不需要与函数名同名的函数体，只需要实现_Validate和_Implementation两个函数即可。


注意事项：
1，Replicated属性只能在服务端修改
Replicated属性只允许服务端修改后通知客户端，而不允许客户端修改Replicated属性后通知到服务端。
参考：Only the server can replicate variables or multicast events to all clients  
https://answers.unrealengine.com/questions/459423/change-variable-in-client-want-server-to-see-it-bu.html

2，Server或者Client函数参数只能时指针或者引用，而不能是对象
比如如果参数是FString，那么必须是引用：const FString& Str，而不能是FString对象。

3，HUD的构造函数在服务端也会执行，但是DrawHUD()函数不会在服务端执行。
也就是说你要在HUD中判断当前程序是客户端还是服务端，可以不用考虑DrawHUD()函数。

    
其他参考文章：  
属性同步：
http://blog.csdn.net/yangxuan0261/article/details/54766955  
RPC：  
http://blog.csdn.net/yangxuan0261/article/details/54766955

