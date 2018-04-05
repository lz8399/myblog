+++
title= "[MacOS]编译Mac版本的protobuf2.6步骤"
date= "2018-03-03T18:35:02+08:00"
categories= ["MacOS"]
tags= ["MacOS"]
keywords= ["Mac", "Protobuf"]
+++


假设是在全新的Mac系统上安装protobuf 2.6

1，安装brew

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    
2，安装automake

    brew install automake

3，安装libtool

    brew install libtool
    
4，安装protobuf

分两种方式：  
4.1，brew安装

    brew install protobuf

4.2，下载protobuf源码，并cd到源码目录

    sh autogen.sh
    
然后会提示：

    Failed to connect to googletest.googlecode.com port 80: Operation timed out

这是因为autogen.sh中有去下载gtest，但是这个gtest地址是404，即使开启了科学上网工具。

解决办法：手动下载gtest并放到protobuf根目录，并改名为gtest。下载地址：https://github.com/google/googletest/tree/release-1.5.0
    
然后依次执行以下命令：

    sh autogen.sh
    
    ./configure

    make
    
    make check

    sudo make install

最后检测是否安装成功：

    protoc --version


### 常见问题

###### 问题1

    ./autogen.sh: 48: autoreconf: not found
    
解决办法：
    
    brew install automake

###### 问题2

    configure.ac:17: error: possibly undefined macro: AC_PROG_LIBTOOL
    If this token and others are legitimate, please use m4_pattern_allow.
    See the Autoconf documentation.
    autoreconf: /usr/bin/autoconf failed with exit status: 1
    
解决办法：

    brew install libtool
    
保险一点，同时安装下：

    brew install libsysfs-dev
    
### 参考资料
mac 安装 protocol buffer（2.6.1版） 教程  
http://www.wangquanwei.com/2017-06-10-1.html
    
Google Protobuf - Mac OS X and iOS Support  
https://gist.github.com/BennettSmith/9487468ae3375d0db0cc
