---
title: "[UE4]Unable to load module 'HTTPChunkInstaller'"
date: "2017-06-03T17:06:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

打包正常，但是启用游戏时弹框提示：Unable to load module 'HTTPChunkInstaller'。

##### 问题原因：
HTTPChunkInstaller是4.16才加入的plugin，如果在4.16之前的版本中build，且build输出目录是4.16版本使用过的输出目录，则会出现这个错误。

##### 解决办法：
新建一个空白的build输出目录，以免版本不同导致的build输出文件干扰。

***
`梧桐更兼细雨，到黄昏、点点滴滴。者次第，怎一个、愁字了得。—李清照《声声慢》`