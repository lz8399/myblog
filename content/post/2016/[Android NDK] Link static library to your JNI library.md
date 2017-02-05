---
title: "[Android NDK] Link static library to your JNI library"
date: "2016-10-15T01:09:40+08:00"
categories:
- Android
tags:
- NDK
---

http://blog.marcingil.com/android-ndk-link-static-library-to-your-jni-library/

When you're developing an application that needs to use a custom, native precompiled library (the .a file) together with your gluing JNI interface maybe you're wondering how to link it.
It's fairly simple and you can even make it target architecture aware (separate precompiled libraries for arm, arm-v7a, x86).
In your module (I'm using Android Studio) you should have a jnidirectory, like this:

    project /
      + module
        + src
          + main
            + jni           # JNI source files here and other native sources here
              | Android.mk
              | Application.mk
              | Xjni.c
              + x86         # target x86 ABI directory
                | libX.a    # x86 precompiled static library
              + armeabi
                | libX.a
              + armeabi-v7a # and so forth
              + mips
              
Now for the contents of `Android.mk`:

    LOCAL_PATH := $(call my-dir)
    # prepare libX
    include $(CLEAR_VARS)
    LOCAL_MODULE    := libX
    LOCAL_SRC_FILES := $(TARGET_ARCH_ABI)/libX.a
    include $(PREBUILT_STATIC_LIBRARY)

    # build JNI
    include $(CLEAR_VARS)
    LOCAL_STATIC_LIBRARIES := X
    LOCAL_MODULE    := Xjni
    LOCAL_SRC_FILES := Xjni.c
    include $(BUILD_SHARED_LIBRARY)
    
Now from the project root folder issue a command:

    NDK_PROJECT_PATH=module/src/main ndk-build 
    
and you're set. In the `module/src/main/libs` directory you should have your compiled JNI library that will be copied by `gradle assemble` to your APK. For all target ABIs.
Have fun!
