---
title: "[UE4]Generate Visual Studio工程时如何指定VS版本"
date: "2017-05-26T17:17:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4 generate visual studio project file、VS2017

UE4 generate visual studio project file cmd

    "%UE4PATH%\Engine\Build\BatchFiles\GenerateProjectFiles.bat" %~dp0\MyProject.uproject -2017

<font color=red>注意：GenerateProjectFiles.bat在源码编译的UE4中，Launcher安装版本的UE4没有GenerateProjectFiles.bat。</font>
    
参考：  
https://answers.unrealengine.com/questions/579186/what-about-visual-studio-2017-in-ue4.html

官方文档：  
https://docs.unrealengine.com/latest/INT/Programming/UnrealBuildSystem/ProjectFileGenerator/index.html