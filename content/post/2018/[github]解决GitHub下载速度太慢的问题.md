+++
title= "[github]解决GitHub下载速度太慢的问题"
date= "2018-08-04T17:02:02+08:00"
categories= ["VersionControl"]
tags= ["Git"]
+++

以下两步缺一不可

##### 步骤一
从GitHub下载文件一直非常慢，查看下载链接发现最终被指向了Amazon的服务器，下载地址是`http://github-cloud.s3.amazonaws.com/`，从国内访问Amazon非常慢，所以总是下载失败，解决方法时更改host文件，使该域名指向香港的服务器：

更改hosts文件：

Windows  
更改C:\Windows\System32\drivers\etc\hosts文件，在文件中追加`219.76.4.4 github-cloud.s3.amazonaws.com`, 将域名指向该IP即可

Mac  
执行 sudo vi /etc/hosts 追加 `219.76.4.4 github-cloud.s3.amazonaws.com`

最后执行`ipconfig /flushdns`命令，刷新 DNS 缓存。



##### 步骤二
https://www.ipaddress.com/ 使用 IP Lookup 工具获得下面这两个github域名的ip地址，该网站可能需要梯子，输入上述域名后，分别获得`github.com`和`github.global.ssl.fastly.net`对应的ip，比如 192.30.xx.xx 和 151.101.xx.xx 。准备工作做完之后，打开的hosts文件中添加如下格式，IP修改为自己查询到的IP：

    192.30.xx.xx github.com
    151.101.xx.xx github.global.ssl.fastly.net

最后执行`ipconfig /flushdns`命令，刷新 DNS 缓存。修改后的下载速度能达到 2MB/S 以上。

参考自：https://blog.csdn.net/qing666888/article/details/79123742