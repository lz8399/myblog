+++
title= "[UE4]Actor Lifecycle"
date= "2018-08-20T12:33:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Actor Lifecycle", "Garbage Collection"]
+++

##### EndPlay、BeginDestroy、Destroy 的调用时机

+ 如果要获取 Actor 销毁时的准确时间点，建议重写 Destroy() 函数，而不是EndPlay()、BeginDestroy()。
+ 官方文档上说 EndPlay 会在执行Destroy的时候触发，但实际上并不会（至少4.20版本中测试过不会），而是当 Actor 所在场景销毁时（比如退出编辑器）才会调用。
+ BeginDestroy()、IsReadyForFinishDestroy()、FinishDestroy() 是在执行垃圾回收时才会触发的函数，而不是对象被 Destroy 后立即执行的函数。

##### Difference between BeginPlay and StartPlay of GameModeBase

+ BeginPlay() inherit in Actor, and StartPlay() inherit in GameModeBase.
+ GameModeBase::BeginPlay() triggered before GameModeBase::StartPlay().

官方文档  
https://docs.unrealengine.com/en-us/Programming/UnrealArchitecture/Actors/ActorLifecycle