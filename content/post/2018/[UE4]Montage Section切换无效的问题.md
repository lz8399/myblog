+++
title= "[UE4]Montage Section切换无效的问题"
date= "2018-02-11T21:58:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

keywords: UE4 Montage Section not working

问题现象：  
SetNextSection在编辑器中运行正常，但是在打包版本中无效。

解决办法：  
将SetNextSection替换为JumpToSection。

参考自：Montage unwanted section switching  
https://answers.unrealengine.com/questions/172537/montage-unwanted-section-switching.html