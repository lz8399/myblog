+++
title= "[UE4]转载：联机烘焙"
date= "2018-03-16T18:35:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Joint Baking"]
+++

UE4联机烘焙出现问题和解决方式  
https://blog.csdn.net/shenmifangke/article/details/78394872

UE4联机编译光照  
http://www.cnblogs.com/ghl_carmack/p/8580617.html

如果还是只有在本地编译那么可能会是下列问题造成的：

1、 任务太小，不值得联机编译。  
2、 没有打开File And Printer Sharing。  
3、 如果是Win10的话切换为专用网络，Win7切换为工作网络或者家庭网络。主要是为了确保已经开启了File And Printer Sharing。  
4、 Swarm agent waiting for remotes to become available。一种情况下是它也在自己编译，另外可能就是没有打开File And Printer Sharing。  
5、 其它的问题请参考Swarm Agent Troubleshooting  
