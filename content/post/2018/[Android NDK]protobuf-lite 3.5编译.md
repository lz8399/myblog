+++
title= "[Android NDK]protobuf-lite 3.5编译"
date= "2018-04-19T15:42:02+08:00"
categories= ["Android"]
tags= ["NDK", "Android", "protobuf"]
+++

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
