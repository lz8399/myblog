+++
title= "[VersionControl]svn常用命令行命令"
date= "2018-02-06T10:16:02+08:00"
categories= ["VersionControl"]
tags= ["SVN"]
+++


检出 （简写：svn co）

    svn checkout url --username=*** --password=*** path     //第一次check out
    svn checkout url    //不是第一次check out


添加

    svn add file    //添加指定文件
    svn add *.cpp  //添加当前目录下的所有的cpp文件
    svn add * --no-ignore 文件夹   //添加指定文件夹下的所有文件（包括忽略的文件类型.a、.pdb等）
    
提交（简写：svn ci）
    
    svn commit -m "LogMessage"

更新（简写：svn up）

    svn update .    //更新当前目录
    svn update test.cpp     //更新指定文件
    svn update -r 200 test.cpp      //更新指定文件到指定版本


回退

    svn revert . --depth=infinity   //整个目录回退
    
回退到旧版本并提交
    
    svn update      //回退前要保证版本更新到最新，假设最新版本为150，准备回退到140
    svn merge -r 150:140 .
    svn commit -m "Rolled back to r140"

清理

    svn cleanup
    
查看日志

    svn log path    //查看目录的log
    svn log test.php    //查看文件的log
    svn log path -l 10  //查看log前10条
    svn log -q      //只输出版本号、时间、作者 而不输出日志
    svn log -l 5 --xml >> aaa.xml   //log输出到xml文件
