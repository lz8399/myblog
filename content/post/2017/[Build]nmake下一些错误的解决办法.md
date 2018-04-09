+++
title= "[Build]nmake下一些错误的解决办法"
date= "2017-12-09T15:32:28+08:00"
categories= ["Build"]
tags= ["CMake"]
+++

原文：http://10305101ivy.blog.163.com/blog/static/584765892012227322607

最近编译工程用到了windows下nmake工具，遇到了很多的问题，在网上苦寻答案，终于得到解决。现在把遇到的问题及解决办法写下来，希望给大家一些帮助。

##### 1.NMAKE:fatal error U1077.“cl.exe” return code 0xc0000135

产生原因：在安装visual studio的时候没有勾选注册环境变量导致的。

解决办法：在系统环境变量中加入visual studio的安装路径：vs安装路径\VC\Bin,以及vs安装路径\Common7\IDE

##### 2.NMAKE:fatal error U1077. return code 0x2

产生原因：找不到代码文件中包含的头文件

解决办法：cmd下进入到vs安装路径\VC\Bin下，执行vcvars32,此时会执行vcvas32.bat自动为vs设置环境变量

##### 3.NMAKE:fatal error U1077. return code 0x460

产生原因：你的工程中连接了一个lib文件，链接的时候却出现不能解析的外部符号。可能问题是你包含的lib是错的，或者有不兼容问题。我的问题就是后者，我的系统的32位的，但是链接了一个64位的lib.

解决办法：链接正确的lib