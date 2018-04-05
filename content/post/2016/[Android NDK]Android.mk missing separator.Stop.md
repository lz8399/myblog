---
title: "[Android NDK]Android.mk missing separator.Stop"
date: "2016-10-15T15:30:40+08:00"
categories:
- Android
tags:
- NDK
- Error
---

android NDK编译代码时，命令行提示错误：

`jni/Android.mk:21: *** missing separator.  Stop.`

##### 原因有以下几点：

1，`$符号之前必须有一个空格，不能跟前面的字符连在一起`。如果$是该行的第一个字符，前面可以不用空格。
例子（正常）：

    LOCAL_PATH := $(call my-dir)  
    include $(CLEAR_VARS) 

错误写法：

    LOCAL_PATH :=$(call my-dir)  
    include$(CLEAR_VARS) 


2，`每行结尾处不能有空格`。
例子（正常）：

    COMPILER_SRC_FILES :=  \

错误写法：

    COMPILER_SRC_FILES :=  \  
