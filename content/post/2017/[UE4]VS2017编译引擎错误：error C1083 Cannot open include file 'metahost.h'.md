+++
title= "[UE4]VS2017编译引擎错误：error C1083 Cannot open include file 'metahost.h'"
date= "2017-12-07T14:46:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "VisualStudio"]
+++


编译错误：

	c:\memspect\vsassert\pch.h(20): fatal error C1083: Cannot open include file: 'metahost.h': No such file or directory

解决办法：  
重新打开VS2017的安装器，下面的都勾上，然后安装。
{{< figure src="/img/20171207-[UE4]VS2017编译引擎错误：error C1083 Cannot open include file 'metahost.h'/[UE4]VS2017编译引擎错误：error C1083 Cannot open include file 'metahost.h'-01.jpg">}}

参考：
https://blogs.msdn.microsoft.com/calvin_hsia/2017/02/13/cannot-open-include-file-metahost-h-no-such-file-or-directory/