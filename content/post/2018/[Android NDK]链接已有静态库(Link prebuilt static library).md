+++
title= "[Android NDK]链接已有静态库(Link prebuilt static library)"
date= "2018-04-18T18:18:02+08:00"
categories= ["Android"]
tags= ["NDK", "Android"]
+++

引用静态库头文件：

    LOCAL_C_INCLUDES += ../include/

引用静态库：

    LOCAL_LDLIBS += ../lib/libMyBoostLib.a

Android.mk：

    LOCAL_PATH := $(call my-dir)

    include $(CLEAR_VARS)
    LOCAL_MODULE    := helloJNI
    LOCAL_SRC_FILES := mainActivity.cpp

    LOCAL_C_INCLUDES := $(LOCAL_PATH)/inc/
    LOCAL_LDLIBS    := -llog -L$(LOCAL_PATH)/inc/ -lMyLibrary
    include $(BUILD_SHARED_LIBRARY)

Include prebuilt static library  
https://stackoverflow.com/questions/18983037/include-prebuilt-static-library

***
`故兵无常势，水无常形。能因敌变化而取胜者，谓之神。故五行无常胜，四时无常位，日有短长，月有死生。`