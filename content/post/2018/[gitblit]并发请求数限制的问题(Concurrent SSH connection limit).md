+++
title= "[gitblit]并发请求数限制的问题(Concurrent SSH connection limit)"
date= "2018-08-07T17:30:02+08:00"
categories= ["VersionControl"]
tags= ["gitblit"]
+++

问题现象：  
当同时 pull 或者 push 的人数较多时，只有第一个用户正常，其他用户会卡住。

解决办法：  
修改配置文件`data/gitblit.properties`，添加：

    execution.defaultThreadPoolSize = 10
    
`defaultThreadPoolSize` 默认为0。


参考自：  
Concurrent push not working  
https://github.com/gitblit/gitblit/issues/905