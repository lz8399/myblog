+++
title= "[VersionControl][git]error unpack failed error Missing commit XXX"
date= "2018-07-19T14:43:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

原文：https://blog.csdn.net/shuilengqingqiu/article/details/77945658

git提交代码时出现错误：error : unpack failed : error Missing commit XXX，XXX代表提交的版本号。

原因：本地索引出错。

解决方法：

1. git gc

2. git pull --rebase（执行之前要先把本地的修改stash 或者commit。过程中遇到冲突需要先解决冲突，再git add .）

3. git push