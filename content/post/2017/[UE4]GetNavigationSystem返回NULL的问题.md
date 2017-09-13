---
title: "[UE4]GetNavigationSystem返回NULL的问题"
date: "2017-09-12T15:31:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Client、UNavigationSystem、自动寻路、Dedicated Server

在有独立服务器的情况下，客户端默认关闭了Navigation，导致在客户端获取NavigationSystem时始终返回NULL。

    UNavigationSystem* const NavSys = GetWorld()->GetNavigationSystem();
    
解决办法：  
打包之前勾选工程设置的中的Allow Client Side Navigation（Project Settings -》 Engine -》 Navigation System）：
{{< figure src="/img/20170912-[UE4]GetNavigationSystem返回NULL的问题/[UE4]GetNavigationSystem返回NULL的问题-01.jpg">}}

注意事项：  
如果有独立服务器，建议寻路只在一端执行，要么客户端要么服务端，如果两边同时开启了寻路，会导致角色移动时有明显的抖动。