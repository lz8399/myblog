---
title: "[git]错误：fatal Not a git repository (or any of the parent directories)"
date: "2016-12-25T21:00:02+08:00"
categories:
- VersionControl
tags:
- Git
---

我用git add file添加文件时出现这样错误：

    fatal: Not a git repository (or any of the parent directories): .git

提示说没有.git这样一个目录，执行命令：

    git init

就可以了！