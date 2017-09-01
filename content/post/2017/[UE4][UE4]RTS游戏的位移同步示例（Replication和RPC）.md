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


    

    
其他参考文章：  
属性同步：
http://blog.csdn.net/yangxuan0261/article/details/54766955  
RPC：  
http://blog.csdn.net/yangxuan0261/article/details/54766955

