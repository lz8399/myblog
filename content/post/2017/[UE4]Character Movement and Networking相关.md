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

***
`人们常常用咄咄逼人来掩饰弱点，真正持久的力量存在于忍受中，只有软骨头才急躁粗暴，他们因此丧失了人的尊严。我等待，我观看。恩惠也许来，也许不来。也许这种既平静又不平静的等待就是恩惠的使者，抑或恩惠本身。──弗兰茨·卡夫卡（FranzKafka）`