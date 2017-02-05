---
title: "[Windows]TortoiseGit安装程序出错：the installer has encountered an unexpected error the error code is 2503"
date: "2016-09-11T22:36:40+08:00"
categories:
- Windows
tags:
- TortoiseGit
---

安装TortoiseGit时提示一下错误：

    the installer has encountered an unexpected error the error code is 2503

#### 原因：
`win8、win10的权限问题`

#### 解决办法：
命令行运行 

    msiexec /package E:\TortoiseGit-2.2.0.0-64bit.msi