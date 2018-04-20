+++
title= "[Android NDK]protobuf-lite 2.6编译与protoc生成代码编译"
date= "2018-02-11T12:27:02+08:00"
categories= ["Android"]
tags= ["NDK", "Android", "protobuf"]
+++

##### Protobuf源码与protoc生成代码编译成一个静态库

工程结构：

    MyProj
      |-jni
        |-  Android.mk
        |-  Application.mk
        |-  google
            |-  protobuf
            |-      io
            |-      stubs
        |-  proto_gen_src

其中，google为protobuf的源码；proto_gen_src为protoc生成的代码，即：*.pb.cc。
        
Android.mk

    LOCAL_PATH := $(call my-dir)  
    include $(CLEAR_VARS)  
    CC_LITE_SRC_FILES := 										\
    google/protobuf/stubs/common.cc								\
    google/protobuf/stubs/once.cc                                \
    google/protobuf/extension_set.cc                             \
    google/protobuf/generated_message_util.cc                    \
    google/protobuf/message_lite.cc                              \
    google/protobuf/repeated_field.cc                            \
    google/protobuf/wire_format_lite.cc                          \
    google/protobuf/io/coded_stream.cc                           \
    google/protobuf/io/zero_copy_stream.cc                       \
    google/protobuf/io/zero_copy_stream_impl_lite.cc  

      
    # C++ full library  
    # =======================================================  
    #include $(CLEAR_VARS)  
      
    LOCAL_MODULE := MyProj.ndk
    LOCAL_MODULE_TAGS := optional  
      
    LOCAL_CPP_EXTENSION := .cc  
    
    #protobuf源码目录
    LOCAL_SRC_FILES += \
    $(CC_LITE_SRC_FILES)

    #protoc生成代码的目录
    MY_CPP_LIST := $(wildcard $(LOCAL_PATH)/proto_gen_src/*.cpp)
    MY_CPP_LIST += $(wildcard $(LOCAL_PATH)/proto_gen_src/*.cc)
    LOCAL_SRC_FILES += $(MY_CPP_LIST:$(LOCAL_PATH)/%=%)
      
    LOCAL_CFLAGS := -march=armv7-a -mfloat-abi=softfp -DGOOGLE_PROTOBUF_NO_RTTI     #-DGOOGLE_PROTOBUF_NO_RTTI  
      
    include $(BUILD_STATIC_LIBRARY)
    
Application.mk
    
    APP_STL := gnustl_static  
    APP_ABI := armeabi-v7a armeabi  
    APP_PROJECT_PATH := ./  
    APP_BUILD_SCRIPT := ./jni/Android.mk  

最后在MyProj目录下执行命令：

    ndk-build
    
最后生成的静态库MyProj.ndk.a所在目录为：

    MyProj\obj\local\armeabi\MyProj.ndk.a
    MyProj\obj\local\armeabi-v7a\MyProj.ndk.a
    
##### 只编译Protobuf静态库
在上述Android.mk中去掉以下代码：

    #protoc生成代码的目录
    MY_CPP_LIST := $(wildcard $(LOCAL_PATH)/proto_gen_src/*.cpp)
    MY_CPP_LIST += $(wildcard $(LOCAL_PATH)/proto_gen_src/*.cc)
    LOCAL_SRC_FILES += $(MY_CPP_LIST:$(LOCAL_PATH)/%=%)
    
##### 只编译protoc生成代码静态库
在上述Android.mk中去掉以下代码：

    #protobuf源码目录
    LOCAL_SRC_FILES += \
    $(CC_LITE_SRC_FILES)
    