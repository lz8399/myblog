---
title: "[UE4]exec error  one or more of the modules specified using the '-module' argument could not be found"
date: "2016-12-27T15:16:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

编译代码是提示错误：

    exec: error : one or more of the modules specified using the '-module' argument could not be found  

原因：  
没有关闭UE4Editor就在编译代码。不是必现，感觉是UE4的bug。

