+++
title= "[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)"
date= "2017-02-25T20:33:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Replication", "Relicate", "reliable", "RPC", "RTS Movement", "Dedicated Server", "属性同步" ]
+++

下面步骤假设是以development模式来构建，步骤和shipping模式没差异。
 
下面步骤中假设我们自己的UE4工程名叫：MyProject
##### 1，下载源码及编译
需要现在unrealengine官网上注册并加入github开发组才有权限进入下面地址。  
https://github.com/EpicGames/UnrealEngine/tags  

{{< alert warning >}}注意：编译专用服务器，只能用源码编译版本的引擎，安装版本的引擎无法编译Server。{{< /alert >}}


打开页面后下载一个最新的release版本，解压出来后先运行Setup.bat，会自动下载资源文件，大概有几个G，下载完以后，然后再运行GenerateProjectFiles.bat，会生成VS工程文件，这里假设你已经安装好了VS，我用的vs2015旗舰版，生成完以后打开VS，build类型选择debuggame editor或者development editor，并编译。
 
##### 2，切换工程的UE4版本
右键点击你的UE4工程文件MyProject.uproject -》 Switch Unreal Engine version，选择刚刚编译出来的UE4，切换版本以后，再右击*.uproject并选择：Generate Visual Studio project files，最后启动VS，启动VS之后再选择一种build类型来编译工程并启动，这里测试用的是development editor类型。
 
##### 3，cook client content
上面第二步编译并启动运行工程后，这一步来打包客户端（官方文档上叫cook client content），方法和正常客户端版本打包的步骤一样：  
Package Project -》 Windows -》 Windows x64。
{{< figure src="/img/20170225-[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)/[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)-01.jpg">}}
有人可能会问，安装版本的UE4为什么有没PS4、Xbox等打包选项？是的，只有源码编译的UE4才有这些选项。  
这里我们假设打包时选择的输出目录为：D:/PackageTest/，那么输出的客户端exe文件就在{{< hl-text green >}}D:/PackageTest/WindowsNoEditor/MyProject/Binariesk/Win64/MyProject.exe{{< /hl-text >}}  
这个目录位置会在后面步骤中用到。

如果不cook client content，则后面启动服务端时会报错：
{{< alert danger >}}Error: The global shader cache file 'F:/EpicGames/UnrealEngine/Engine/GlobalShaderCache-PCD3D_SM5.bin' is missing.{{< /alert >}}

{{< hl-text danger >}}还有一个纯蓝图UE4工程的构建bug问题：{{< /hl-text >}}  
这个问题v4.7版本时还存在，当前最新版本不知道解决没有。  
问题现象是：如果用VS构建之前不添加一个自定义的C++代码，那么构建出来的版本会有问题。  
解决办法：在VS构建server版本之前，在UE4 Editor中添加一个C++代码，这个代码随意，只要是C++代码就行（比如添加一个自定义HUD的class），内容默认，不需要编辑。  
添加C++方法是：File -》 Add Code to Project。  
由于我这里演示的是C++工程，所以不需要添加再添加C++ class。  
 
打包之前记得GameMode和Map是否设置正确了，如果不使用默认的话。
{{< figure src="/img/20170225-[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)/[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)-02.jpg">}}
{{< alert warning >}}如果这里不设置，默认为空，则客户端进入服务端后会黑屏。{{< /alert >}}

##### 4，添加Server.target.cs配置文件
这一步是关键步骤。  
从官网教学项目ShooterGame中拷贝一个文件：  
{{< hl-text green >}}\Epic Games\Launcher\VaultCache\ShooterGame_‘版本号’\data\Source\ShooterGameServer.Target.cs{{< /hl-text >}}

没有安装的话，新建一个文本文件，并命名为{{< hl-text blue >}}MyProjectServer.Target.cs{{< /hl-text >}}，复制粘贴以下代码，并将代码文件放在\MyProject\Source\目录下（与其他Target.cs文件同一目录）：

    // Copyright 1998-2017 Epic Games, Inc. All Rights Reserved.

    using UnrealBuildTool;
    using System.Collections.Generic;

    [SupportedPlatforms(UnrealPlatformClass.Server)]
    public class ShooterGameServerTarget : TargetRules
    {
        public ShooterGameServerTarget(TargetInfo Target) : base(Target)
        {
            Type = TargetType.Server;
            bUsesSteam = true;

            ExtraModuleNames.Add("ShooterGame");
        }
    }

在此基础上需要修改的地方三个地方：

+ 1，类名修改MyProjectServerTarget ；
+ 2，构造方法修改MyProjectServerTarget；
+ 3，ExtraModuleNames.Add("ShooterGame");修改为：ExtraModuleNames.Add("MyProject");

{{< alert warning >}}注意：这段代码是4.16及以后的版本，4.16之前的版本用上面代码无法编译。{{< /alert >}}

##### 5，构建Server版本
首先，关掉VS，然后右击工程文件*.uproject-》Generate Visual Studio project files，之所以要重新生成VS工程文件，是因为要确保上一步添加的Target.cs文件能够在编译中生效。

打开VS后，选择build类型Development Server，然后构建。
{{< figure src="/img/20170225-[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)/[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)-03.jpg">}}

构建完毕以后，输出的server.exe文件位置在：{{< hl-text green >}}/MyProject/Binaries/Win64/MyProjectServer.exe。{{< /hl-text >}}  
然后拷贝这个MyProjectServer.exe文件到上面第3步中提到的目录位置：{{< hl-text green >}}D:/PackageTest/WindowsNoEditor/MyProject/Binaries/Win64/{{< /hl-text >}}目录下。  
此时，该目录就会同时存在两个exe文件：{{< hl-text blue >}}MyProject.exe{{< /hl-text >}}和{{< hl-text blue >}}MyProjectServer.exe{{< /hl-text >}}。
 
如果MyProjectServer.exe不和MyProject.exe放在一起，则启动server时会报错（下面只是其众多错误信息中的一条）：  
{{< hl-text danger >}}default Property warning and errors:{{< /hl-text >}}  
{{< hl-text danger >}}Error: CDO Constructor (WidgetComponent): Failed to find /Engine/EngineMaterials/Widget3DPassThrough_Translucent{{< /hl-text >}}  

##### 6，启动Server
到此为止，已经从构建UE4服务端这个深坑中爬出来了。。。  
命令行启动：

    MyProjectServer.exe -log

执行后会看到弹出一个新的CMD窗口，并看到相关打印信息。  
如果不带-log参数，则不会显示命令行窗口，只有一个后台进程。  
{{< figure src="/img/20170225-[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)/[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)-04.jpg">}}

##### 7，client连接server
这一步很简单，启动客户端游戏后（双击打包生成的MyProject.exe或者从UE4 Editor中启动游戏均可），按~键，输入：{{< hl-text green >}}open   127.0.0.1:7777{{< /hl-text >}}，即可连接上服务端，7777是端口号。如果是shipping模式，是没有这种命令行的，连接服务端需要手动写相关的逻辑代码。

这样UFUNCTION(Server, Reliable, WithValidation)函数就可以与客户端独实现同步了。

{{< alert warning >}}注意的是：按~键打开游戏的命令行只对development和debug模式有效，shipping模式无效，另外shipping下也会关闭自带的同步机制（开头提到的）。{{< /alert >}}

##### 常见问题
如果出现以下错误提示，原因是客户端和服务端版本不匹配，比如编译完客户端之后又改过代码，然后再编译服务端。  
{{< hl-text danger >}}LogNet: NotifyControlMessage: Client connecting with invalid version. LocalNetworkVersion: -629807355, RemoteNetworkVersion: 1642249361{{< /hl-text >}}

##### 参考资料

Dedicated Server Guide (Windows & Linux)  
https://wiki.unrealengine.com/Dedicated_Server_Guide_(Windows_%26_Linux)


***
`自古美人如名将，不许人间见白头。`
