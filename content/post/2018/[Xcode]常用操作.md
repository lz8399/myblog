+++
title= "[Xcode]常用操作"
date= "2018-03-07T20:29:02+08:00"
categories= ["Xcode"]
tags= ["iOS"]
keywords= ["iOS", "Mac", "Xcode"]
+++

##### 构建
command + R

###### 清理工程
command + shift + K

###### 当前工程根目录的环境变量（.xcworkspace文件所在目录）

    $(SRCROOT)
    
    
###### 头文件搜索路径
Always Search User Paths  是否优先使用User Header Search Paths  
Header Search Paths  编译器的头文件目录  
User Header Search Paths  自己工程的头文件目录  

##### 修改编译输出目录
Build Settings -> Build Locations -> Build Products Path  
修改后需要重启xcode才会生效。

参考：http://blog.csdn.net/tintinr/article/details/50936313

iOS 静态库制作（Xcode9.0）  
http://blog.csdn.net/wanna_dance/article/details/78687676
