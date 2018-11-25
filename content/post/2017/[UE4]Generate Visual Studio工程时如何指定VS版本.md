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

【2017-08-31记】  
今天发现4.17版本用上述方法貌似有问题，会打印一个警告，且最终没有生成任何文件：

     warning MSB3884: Could not find rule set file "ManagedMinimumRules.ruleset"
     
解决办法：  
执行以下命令，末尾参数2017即表示指定VS2017：

    D:/UnrealEngine-4.17.1-release/Engine/Binaries/DotNET/UnrealBuildTool.exe  -projectfiles -project="D:/MyProject/MyProject.uproject" -game -engine -progress -2017
    
另外UnrealBuildTool.exe在Launcher安装版本也存在，不需要源码编译的版本。
    
参考：  
https://answers.unrealengine.com/questions/579186/what-about-visual-studio-2017-in-ue4.html

官方文档：  
https://docs.unrealengine.com/latest/INT/Programming/UnrealBuildSystem/ProjectFileGenerator/index.html

##### Visual Studio 所需的最低 Windows SDK 版本
【2018-11-25】  
4.18需要安装 Windows SDK 8.1，否则无法 Generate VS project file；  
4.20不需要安装 Windows SDK 8.1，只需点选最新版本的 Windows SDK 即可。

***
`琵琶弦上说相思，当时明月在，曾照彩云归。---晏几道《临江仙》`