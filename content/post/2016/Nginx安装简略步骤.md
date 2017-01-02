---
title: "Nginx安装简略步骤"
date: "2016-05-26T22:30:02+08:00"
categories:
- Linux
- Http
tags:
- nginx
- linux
- install
---


### 安装依赖
    $ yum install -y zlib-devel 
    $ yum install -y pcre-devel
    $ yum install -y ssl
    $ yum install -y gcc

### 编译&安装
    $ ./configure
    $ make
    $ make install

默认安装目录：

    /usr/local/nginx/
	
nginx的bin目录：

    /usr/local/nginx/sbin

link到bin目录

    $ ln /usr/local/nginx/sbin/nginx /usr/local/bin/nginx

### 开机自动启动
如果使用编译版本，貌似配置器比较复杂。建议用yum安装，这样安装后就是自动启动且帮你link好了。

