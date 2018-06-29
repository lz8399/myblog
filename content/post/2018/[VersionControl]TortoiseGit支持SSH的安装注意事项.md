+++
title= "[VersionControl]TortoiseGit支持SSH的安装注意事项"
date= "2017-12-25T18:19:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

在安装完以后的配置选项中，SSH选择OpenSSH：
{{< figure src="/img/20171225-[VersionControl]TortoiseGit支持SSH的安装注意事项/[VersionControl]TortoiseGit支持SSH的安装注意事项-01.jpg">}}

如果选择PuTTY，则每次更新或提交时，都需要输入密码。  
除了在安装配置页面设置，也可以在安装完毕以后，右键 -》 TortoiseGit -》 Settings -》Network -》 SSH -》 修改为：`"ssh.exe"` 或者 `"Git安装目录\usr\bin\ssh.exe"`

##### 生成公钥

命令（ssh-keygen.exe 位于 `Gi安装目录\usr\bin` 目录下）

	ssh-keygen -t rsa -C "mysshkey"
    
执行后敲三次回车，即可生成SSH公钥和私钥。
	
***
`我感到难过，不是因为你欺骗了我，而是因为我再也不能相信你了。----尼采《天才的激情与感悟》`