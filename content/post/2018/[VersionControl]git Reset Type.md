+++
title= "[VersionControl]git Reset Type"
date= "2018-06-28T18:38:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

##### 概述

Reset Type有三种类型：Soft、Mixed、Hard。

理解Reset Type之前，先解释下以下术语：

+ `HEAD` 这是当前分支版本顶端的别名，也就是在当前分支你最近的一个提交
+ `Index` Index也被称为staging area，是指一整套即将被下一个提交的文件集合。他也是将成为HEAD的父亲的那个commit
+ `Working Directory` 代表你正在工作的那个文件集，又称作Working Tree。

三个Reset级别的意思分别是：

+ `Soft` # 还原 HEAD
+ `Mixed` # 还原 HEAD、Index # 默认参数
+ `Hard` # 还原 HEAD、Index、Working Directory

##### 应用

如果本地有commit，但是没有push，此时想把这个commit 回退掉，则：右键需要回退的SHA-1 -》 Reset "master" to this。
{{< figure src="/img/20180628-[VersionControl]git Reset Type/[VersionControl]git Reset Type-01.png">}}

然后和弹出菜单：
{{< figure src="/img/20180628-[VersionControl]git Reset Type/[VersionControl]git Reset Type-02.png">}}

选择合适的Reset Type，点击OK。

注意事项：  
根据需要选择Reset Type：

+ 若本地无修改，那么就选择 `Soft`;
+ 若本地有修改未commit，那么就选择 `Mixed`;
+ 若本地有修改且已commit，那么就选择 `Hard`;

参考自：git reset soft,hard,mixed之区别深解  
https://www.cnblogs.com/kidsitcn/p/4513297.html