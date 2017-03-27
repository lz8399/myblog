---
title: "[Android NDK]fatal error 'backward_warning.h' file not found"
date: "2016-10-15T01:09:40+08:00"
categories:
- Android
tags:
- NDK
- UE4
- Error
---


android中使用hash_map时报错：
`fatal error: 'backward_warning.h' file not found`

解决办法：
Android.mk添加宏定义

    LOCAL_CFLAGS    :=  -D_GLIBCXX_PERMIT_BACKWARD_HASH 

如果是UE4项目编译android版本，在工程的Build.cs中添加：

    Definitions.Add("_GLIBCXX_PERMIT_BACKWARD_HASH");
