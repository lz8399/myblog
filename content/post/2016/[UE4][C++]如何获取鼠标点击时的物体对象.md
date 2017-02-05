+++
title= "[UE4][CPP]如何获取鼠标点击时的物体对象"
date= "2016-11-10T22:33:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

注册回调函数：

    MyObject->OnClicked.AddDynamic(this, &AExampleActor::DoAthing);