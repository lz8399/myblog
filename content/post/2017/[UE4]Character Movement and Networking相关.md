---
title: "[UE4]Character Movement and Networking相关"
date: "2017-09-15T10:55:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Movement Replicate、Networking、Server、Client、Smooth

引擎对于客户端服务端的位移同步，CharacterMovementComponent::SmoothCorrection()函数中有进行平滑处理。


其他参考资料：  
What is the best way to smooth player movement for network hiccups? Interp? Ease? (no physics)  
https://answers.unrealengine.com/questions/479211/what-is-the-best-way-to-smooth-player-movement-for.html

Authoritative Networked Character Movement  
https://wiki.unrealengine.com/Authoritative_Networked_Character_Movement

Advanced Topic: Adding New Movement Abilities to Character Movement  
https://docs.unrealengine.com/latest/INT/Gameplay/Networking/CharacterMovementComponent/index.html#advancedtopic:addingnewmovementabilitiestocharactermovement

Custom Character Movement Component  
https://wiki.unrealengine.com/Custom_Character_Movement_Component

##### Dedicated Server 的 Movement 优化

如果仅仅为了性能，不希望服务端实时修正客户端坐标，以客户端发过来的坐标为准，可以开启以下选项：

    [/Script/Engine.GameNetworkManager]
     MAXPOSITIONERRORSQUARED=625
     ClientAuthorativePosition=true
     
但是这么做会被外挂 hack

参考自：How am I able to Replicate movement when using "AddMovement Input", but not AddLocalTransform?  
https://answers.unrealengine.com/questions/26116/able-to-replicate-movement-when-using-addmovement.html

##### 运行时期间断开Actor的Replication
比如一个 Character 一开始是在服务端同步的，当他死亡时，之后相关表现希望不再同步，比如布娃娃系统（可破碎网格），如果继续保持同步，会增加服务端计算开销，且布娃娃此时只是客户端表现，并不会驱动服务端数据，所以希望在执行布娃娃破碎之前，断开该Character在客户端服务端之间的Replication。

办法如下：  
服务端在执行布娃娃破碎之前，先执行`AActor::ForceNetUpdate()`，将当前最新状态同步到客户端，然后服务端接着执行`AActor::TearOff`，表示从此时开启，服务端不再同步当前 Actor 给服务端。  
当服务端执行`AActor::TearOff`成功后，客户端会触发回调`AActor::TornOff()`，表示此时客户端可以任意修改当前 Actor 状态，且不会被服务端纠正。


***
`人们常常用咄咄逼人来掩饰弱点，真正持久的力量存在于忍受中，只有软骨头才急躁粗暴，他们因此丧失了人的尊严。我等待，我观看。恩惠也许来，也许不来。也许这种既平静又不平静的等待就是恩惠的使者，抑或恩惠本身。──弗兰茨·卡夫卡（FranzKafka）`