+++
title= "[UE4]UE4Editor.exe crash：dx11 feature level 10.0 is required to run the engine"
date= "2017-12-13T17:52:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Crash", "DX11"]
+++

UE4源码编译的UE4Editor启动时崩溃：

	dx11 feature level 10.0 is required to run the engine （运行引擎需要dx11特性等级）

原因：显卡驱动有问题  
解决办法：卸载显卡驱动，并从AMD或者NVIDIA官网下载对应的驱动。如果更新驱动后还是出现这个问题，则清理掉UE4的源码工程重新编译一次。
另外，如果自己游戏工程是在旧的驱动下面编译的，那么最好把这些编译中间文件删掉，而不要直接使用VS中清理，即使执行“仅清理当前工程”，也会把这个UE4的源码工程清理掉。