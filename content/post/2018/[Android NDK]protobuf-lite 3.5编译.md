+++
title= "[Android NDK]protobuf-lite 3.5编译"
date= "2018-04-19T15:42:02+08:00"
categories= ["Android"]
tags= ["NDK", "Android", "protobuf"]
+++

### NDK编译配置

假设工程结构如下：

    MyProj
      |-jni
        |-  Android.mk
        |-  Application.mk
        |-  protoc_files
            |- *.pb.cc
      |-thirdparty
        |-lib
            |-libprotobuf-lite.a
        |-include
            |-google
               |-protobuf

编译输出的lib叫：mylib，编译时引用编译好的第三方库：protobuf-lite.a
               
Android.mk
    
    LOCAL_PATH := $(call my-dir) 

    include $(CLEAR_VARS)  
      
    LOCAL_MODULE := mylib
    LOCAL_MODULE_TAGS := optional  
      
    LOCAL_CPP_EXTENSION := .cc  
      
    #LOCAL_SRC_FILES += \
    #$(CC_LITE_SRC_FILES)                                         

    MY_CPP_LIST += $(wildcard $(LOCAL_PATH)/protoc_files/*.cc)
    LOCAL_SRC_FILES += $(MY_CPP_LIST:$(LOCAL_PATH)/%=%)


    LOCAL_CFLAGS := -D GOOGLE_PROTOBUF_NO_RTTI=1
    LOCAL_CPPFLAGS := -std=c++11 -D HAVE_PTHREAD=1
    LOCAL_C_INCLUDES = $(LOCAL_PATH)/android
    LOCAL_C_INCLUDES += ${ANDROID_NDK}/sources/cxx-stl/gnu-        libstdc++/4.8/include
    #LOCAL_LDLIBS += -lz -llog
    LOCAL_EXPORT_LDLIBS += -lz
    LOCAL_EXPORT_CFLAGS := $(LOCAL_CFLAGS)
    LOCAL_EXPORT_CPPFLAGS := $(LOCAL_CPPFLAGS)
    LOCAL_EXPORT_C_INCLUDES := $(LOCAL_C_INCLUDES)

    LOCAL_C_INCLUDES += thirdparty/include
    LOCAL_STATIC_LIBRARIES += thirdparty/lib/libprotobuf-lite.a

    #include $(BUILD_SHARED_LIBRARY)
    include $(BUILD_STATIC_LIBRARY)

Application.mk

    APP_STL :=gnustl_static #gnustl_shared # 
    NDK_TOOLCHAIN_VERSION := 4.9
    #APP_ABI := all
    APP_ABI := armeabi-v7a
    LIBCXX_FORCE_REBUILD := true
    APP_PLATFORM:=android-9
    #NDK_DEBUG:=1
    
{{< alert info >}}
编译完成后，项目中需要同时引用mylib.a和protobuf-lite.a，mylib.a编译时并没有将protobuf-lite.a链接进来。
{{< /alert >}}

### 常见问题

如果出现以下错误：

    [armeabi-v7a] Compile++ thumb: protobuf <= common.cc
    C:/Users/jkarr/Downloads/protobuf-
    3.5.0/jni\src/google/protobuf/stubs/common.cc:52:2: error: #error "No 
    suitable threading library available."
    #error "No suitable threading library available."
    ^
    make: *** [C:/Users/jkarr/Downloads/protobuf-3.5.0/obj/local/armeabi-
    v7a/objs/protobuf/google/protobuf/stubs/common.o] Error 1

是因为Android.mk中没有添加：`HAVE_PTHREAD=1`

    LOCAL_CPPFLAGS := -std=c++11 -D HAVE_PTHREAD=1
