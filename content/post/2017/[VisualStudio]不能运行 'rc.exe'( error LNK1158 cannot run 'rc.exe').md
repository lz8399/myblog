+++
title= "[VisualStudio]不能运行 'rc.exe'( error LNK1158 cannot run 'rc.exe')"
date= "2017-12-09T14:44:02+08:00"
categories= ["VisualStudio"]
tags= ["VisualStudio"]
keywords= ["VisualStudio", "LNK1158", "rc.exe"]
+++



先装VS2017，再装VS2015后，使用cmake-gui生成vs solution时报错：

	不能运行 'rc.exe'( error LNK1158: cannot run 'rc.exe')
	
解决办法：

转载自：https://blog.csdn.net/leifeng_soul/article/details/52622584

1. 在D:\Programs\Microsoft Visual Studio 12.0\Common7\IDE中找到devenv.exe。在cmd命令行中切换到该路径，使用命令devenv /ResetSettings将VS2013重置到初始设置。

2. 打开VS2013里面的属性->常规->平台工具，将v120改成v120_xp。
{{< figure src="/img/20171209-[VisualStudio]不能运行 'rc.exe'( error LNK1158 cannot run 'rc.exe')/[VisualStudio]不能运行 'rc.exe'( error LNK1158 cannot run 'rc.exe')-01.png">}}