---
title: "[MySQL]Windows上安装MySQL5.7绿色版"
date: "2017-05-27T13:59:40+08:00"
categories:
- DB
tags:
- MySQL
---

下载：  
https://dev.mysql.com/downloads/mysql/

解压后执行（管理员命令行）：

    mysqld --initialize-insecure --user=mysql
    
然后安装windows服务：

    mysqld install
    
启动：

    net start mysql

修改root密码（首次安装后root还未修改的情况下，即密码为空）

    mysqladmin -u root -p password 123456
    
##### my.ini找不到

Windows 10下，安装MySQL后的my.ini文件位置不再是安装目录的根目录，而是：C:\ProgramData\MySQL\MySQL Server 5.7
	
***
`山映斜阳天接水，芳草无情，更在斜阳外。---范仲淹《苏幕遮》`