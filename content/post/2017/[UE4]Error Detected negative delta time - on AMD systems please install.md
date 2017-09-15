---
title: "[UE4]Error Detected negative delta time - on AMD systems please install"
date: "2017-09-15T10:55:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Fixed Frame rate、Dedicated Server、Crash

如果锁定帧率（Project Settings -》 Engine -》 General Settings -》 Use Fixed Frame Rate），专用服务器启动时会报错：

    LogWindows: Error: Fatal error: [File:D:\sdk\UnrealEngine-4.17.1-release\Engine\Source\Runtime\Engine\Private\UnrealEngine.cpp] [Line: 1385] 
    LogWindows: Error: Detected negative delta time - on AMD systems please install http://files.aoaforums.com/I3199-setup.zip.html - DeltaTime:-0.000259, bUseFixedFrameRate:1, bTimeWasManipulatedDebug:1, FixedFrameRate:30.000000
    
感觉这是个bug，提示我要打AMD的补丁，但是我机器是Intel的U。

