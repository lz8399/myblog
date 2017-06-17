---
title: "[MySQL]Windows上安装MySQL5.7绿色版"
date: "2017-05-27T13:59:40+08:00"
categories:
- DB
tags:
- MySQL
---

下载：  
https://dev.mysql.com/downloads/mysql/s

解压后执行（管理员命令行）：

    mysqld --initialize-insecure --user=mysql
    
然后安装windows服务：

    mysqld install
    
启动：

    net start mysql
    
注意：MySQL官方的5.7绿色版中没有my.ini或my.cnf文件，不知道为什么，在网上找个my.ini文件复制过来放在安装目录下即可。
