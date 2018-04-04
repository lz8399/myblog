+++
title= "[UE4]关卡蓝图继承C++(Creating a C++ Level Blueprint)"
date= "2018-04-04T18:47:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Level Blueprint"]
+++

1，新建一个C++ Actor，继承LevelScriptActor。

2，打开关卡蓝图，点击Class Settings，修改Parent Class。

{{< figure src="/img/20180404-[UE4]关卡蓝图继承C++(Creating a C++ Level Blueprint)/[UE4]关卡蓝图继承C++(Creating a C++ Level Blueprint)-01.jpg">}}

3，然后关卡蓝图中就可以调用自定义LevelScriptActor Class中的UFUNCTION(BlueprintCallable)函数

参考：http://orfeasel.com/creating-a-c-level-blueprint/