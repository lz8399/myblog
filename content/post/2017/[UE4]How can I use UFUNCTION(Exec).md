---
title: "[UE4]How can I use UFUNCTION(Exec)"
date: "2017-03-25T14:47:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

UE4提供了自定义命令的操作，类似GM，方式是创建一个继承CheatManager的自定义类，然在GM函数上加上标识：

    UFUNCTION(Exec)

这样就可以在命令行（按波浪键，shipping模式下无效）中直接调用该函数了。

参考：  
https://answers.unrealengine.com/questions/2642/how-to-add-new-console-command.html  
https://answers.unrealengine.com/questions/45499/ufunctionexec-from-uactorcomponent.html