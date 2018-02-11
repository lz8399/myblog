+++
title= "[Android NDK]protobuf-lite 2.6编译步骤"
date= "2018-02-11T12:27:02+08:00"
categories= ["Android"]
tags= ["NDK", "UE4"]
+++

工程结构：

    MyProj
      |-jni
        |-  Android.mk
        |-  Application.mk
        |-  google
            |-  protobuf
            |-      io
            |-      stubs

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
      
    LOCAL_MODULE := custom_msg.ndk
    LOCAL_MODULE_TAGS := optional  
      
    LOCAL_CPP_EXTENSION := .cc  
      
    LOCAL_SRC_FILES += \
    $(CC_LITE_SRC_FILES)                                         

    MY_CPP_LIST := $(wildcard $(LOCAL_PATH)/gen_source/*.cpp)
    MY_CPP_LIST += $(wildcard $(LOCAL_PATH)/gen_source/*.cc)
    LOCAL_SRC_FILES += $(MY_CPP_LIST:$(LOCAL_PATH)/%=%)
      
    LOCAL_C_INCLUDES := \
    $(LOCAL_PATH)/src  
      
    LOCAL_C_INCLUDES := \
    $(LOCAL_PATH)/android \
    bionic \
    $(LOCAL_PATH)/src \
    $(JNI_H_INCLUDE)  
      
    LOCAL_SHARED_LIBRARIES := \
    libz libcutils libutils  
    LOCAL_LDLIBS := -lz  

      
    LOCAL_CFLAGS := -march=armv7-a -mfloat-abi=softfp -DGOOGLE_PROTOBUF_NO_RTTI     #-DGOOGLE_PROTOBUF_NO_RTTI  
      
    include $(BUILD_STATIC_LIBRARY)  
    
Application.mk
    
    APP_STL := gnustl_static  
    APP_ABI := armeabi-v7a armeabi  
    APP_PROJECT_PATH := ./  
    APP_BUILD_SCRIPT := ./jni/Android.mk  

最后在MyProj目录下执行命令：

    ndk-build