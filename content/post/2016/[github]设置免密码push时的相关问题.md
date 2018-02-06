---
title: "[github]设置免密码push时的相关问题"
date: "2016-11-12T18:44:02+08:00"
categories:
- VersionControl
tags:
- Git
---


1，先在本地生成ssh的公钥，方法如下：

https://gist.github.com/yisibl/8019693

2，在github自己的账号后台中添加上面生成的key，将id_rsa.pub中的所有内容全部copy过来即可。

添加key的页面：https://github.com/settings/keys

3，将https替换为ssh：

    git remote set-url origin git@github.com:USERNAME/REPOSITORY.git 

4，将当前客户端的ssh链接添加到github信任列表

    ssh -T git@github.com

如果不执行这个步骤，会push时会出现错误提示：

    ssh: connect to host github.com port 22: Connection timed out
    fatal: Could not read from remote repository

另外，执行此步骤时必须关掉爬墙工具（你懂的），否则会提示链接超时。