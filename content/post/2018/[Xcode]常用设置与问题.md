+++
title= "[Xcode]常用设置与问题"
date= "2018-03-15T19:00:02+08:00"
categories= ["Xcode"]
tags= ["iOS"]
keywords= ["iOS", "Mac", "Xcode"]
+++

##### 添加头文件目录
{{< figure src="/img/20180315-[Xcode]常用设置与问题/[Xcode]常用设置与问题-01.jpg">}}

Header Search Paths对应系统或者第三方库的头文件；#include <>  
User Header Search Paths 对应用户自己代码的头文件；#include “”  

##### 添加静态库依赖
{{< figure src="/img/20180315-[Xcode]常用设置与问题/[Xcode]常用设置与问题-02.jpg">}}


##### 设置证书签名
https://stackoverflow.com/questions/34346436/xcode-7-2-no-matching-provisioning-profiles-found
{{< figure src="/img/20180315-[Xcode]常用设置与问题/[Xcode]常用设置与问题-03.jpg">}}

##### 清除缓存
点击xcode偏好设置->Locations->Derived Data，点击箭头定位到目标文件夹，将此文件夹清空并清空回收站，再重新编译即可。
有时候这个错误可以通过清理缓存解决：

	Command /usr/bin/codesign failed with exit code 1

##### 编译静态库
http://blog.csdn.net/weidfyr/article/details/50590693

如果用模拟器版本静态库去链接真机版本，可能会出现的错误：

	file was built for archive which is not the architecture being linked (arm64)

解决办法：静态库编译成真机版本

