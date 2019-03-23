---
title: "[UE4]ServerTravel和ClientTravel区别"
date: "2017-06-01T11:05:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Difference：

+ ServerTravel also informs the clients to move along with the server.
+ ClientTravel will be called locally for the client to load a new map. or connect to ip.
+ Browse can load local map via LoadMap ( not for multiplayer ) but there are more things happening in this method. I also want to know more about what it does and what it should be used for.
+ LoadMap should also load a map for a local client

Browse, LoadMap, ServerTravel and ClientTravel?  
https://answers.unrealengine.com/questions/122565/browse-servertravel-and-clienttravel.html

What's the different between absolute travel and relative travel?  
https://answers.unrealengine.com/questions/101284/what-the-different-between-absolute-travel-and-rel.html

What is the difference between ServerTravel and OpenLevel?  
https://answers.unrealengine.com/questions/55477/the-difference-of-the-two-functions.html

PlayerController->ClientTravel()连接远程服务器  
https://answers.unrealengine.com/questions/29017/gamemode-multiplayer-c.html

Seamless and non-seamless travel  
https://docs.unrealengine.com/latest/INT/Gameplay/Networking/Travelling


另外，可以参考官方**ShooterGame**的`APlayerController->ClientTravel()`用法。

***
`山舞银蛇，原驰蜡象，欲与天公试比高。须晴日，看红装素裹，分外妖娆。----毛泽东《沁园春·雪》`