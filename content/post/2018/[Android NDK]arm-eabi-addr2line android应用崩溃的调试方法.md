+++
title= "[Android NDK]arm-eabi-addr2line android应用崩溃的调试方法"
date= "2018-03-29T18:04:02+08:00"
categories= ["Android"]
tags= ["Android NDK"]
+++

原文：https://blog.csdn.net/tommy_wxie/article/details/12841735

1.将ndk中的arm-linux-androideabi-addr2line可执行文件的路径加入配置文件~/.bashrc中，例如：

    export PATH=$PATH:~/dlna/android-ndk-r6b/toolchains/arm-linux-androideabi-4.4.3/prebuilt/linux-x86/bin


2.使配置生效：

    source ~/.bashrc


3.使用工具。例如：

    arm-linux-androideabi-addr2line -C -f -e  ~/workspace/DLNA/libs/armeabi/libctrlpt.so 0003deb4

其中，0003deb4为堆栈信息中pc的值。

 
##### android应用崩溃的调试方法
有两种方法可以分析 crash 的堆栈信息

1，google提供了一个python脚本，可以从
https://github.com/maxme/android-ndk-stacktrace-analyzer
下载这个python脚本，然后使用 adb logcat -d > logfile 导出 crash 的log,使用 arm-eabi-objdump 位于build/prebuilt/linux-x86/arm-eabi-4.2.1/bin下面把so或exe转换成汇编代码，如：arm-eabi-objdump -S mylib.so > mylib.asm,使用脚本

    python parse_stack.py <asm-file> <logcat-file>

2，直接使用NDK下面的arm-linux-androideabi-addr2line 

(D:\android-ndk-r8\toolchains\arm-linux- androideabi-4.4.3\prebuilt\windows\bin\arm-linux-androideabi-addr2line.exe)

例如：

    arm-linux-androideabi-addr2line -C -f -e libxxx.so 0x#####(address)

##### 出现 ??:0 , 没法展示源代码行数的问题

在Android.mk 文件中:

    LOCAL_CFLAGS := -D__STDC_CONSTANT_MACROS -Wl,-Map=test.map -g  


补充2个编译参数  -Wl,-Map=test.map -g .
增加gcc警告和调试标志

执行命令：

    arm-linux-androideabi-addr2line -C -f -e /项目目录/obj/local/armeabi/libfaa_jni.so 0024362e

tip:   
1,注意调试文件的位置在obj目录下,并非libs目录下生成的so文件  
2,0024362e 为出错的机制位置

还有：  
在jni/目录下增加Application.mk 文件， 修改为debug 模式：
    
    APP_OPTIM := debug

具体application.mk 文件的配置见： http://blog.csdn.net/weidawei0609/article/details/6561280

***
`人行阳德，人自报之；人行阴德，鬼神报之；人行阳恶，人自报之；人行阴恶，鬼神害之。  ----孙思邈《大医精诚》 `