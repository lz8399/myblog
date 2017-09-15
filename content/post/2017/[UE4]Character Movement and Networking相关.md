---
title: "[UE4]Character Movement and Networking相关"
date: "2017-09-15T10:55:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Movement Replicate、Networking、Server、Client、Smooth

引擎对于客户端服务端的位移同步，CharacterMovementComponent::SmoothCorrection()函数中有进行平滑处理，但是仍然还有瑕疵，在有DedicatedServer时，客户端的位移还是有明显抖动。  
个人经验是：关掉角色的Movement Replicate，然后在客户端的Tick函数中自己实现位移的平滑同步处理。


其他参考资料：  
What is the best way to smooth player movement for network hiccups? Interp? Ease? (no physics)  
https://answers.unrealengine.com/questions/479211/what-is-the-best-way-to-smooth-player-movement-for.html

Authoritative Networked Character Movement  
https://wiki.unrealengine.com/Authoritative_Networked_Character_Movement

Advanced Topic: Adding New Movement Abilities to Character Movement  
https://docs.unrealengine.com/latest/INT/Gameplay/Networking/CharacterMovementComponent/index.html#advancedtopic:addingnewmovementabilitiestocharactermovement

Custom Character Movement Component  
https://wiki.unrealengine.com/Custom_Character_Movement_Component
