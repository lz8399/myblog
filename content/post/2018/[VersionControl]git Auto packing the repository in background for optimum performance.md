+++
title= "[VersionControl]git Auto packing the repository in background for optimum performance"
date= "2018-11-14T10:49:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

原文：https://blog.csdn.net/xyznol/article/details/51261692

git运行突然提示

    Auto packing the repository in background for optimum performance

查资料，原来是自己本地一些 “悬空对象”太多(git删除分支或者清空stash的时候，这些其实还没有真正删除，成为悬空对象，我们可以使用merge命令可以从中恢复一些文件)

解决：  
1.输入命令：`git fsck --lost-found`，可以看到好多“dangling commit”。  
2.清空他们：`git gc --prune=now`，完成。  
