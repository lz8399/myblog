+++
title= "[UE4]Steam SDK接入相关"
date= "2018-05-09T15:11:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Steam SDK"]
+++

##### 使用第三方plugin

Advanced Sessions Plugin  
https://forums.unrealengine.com/community/community-content-tools-and-tutorials/41043-advanced-sessions-plugin

将该plugin加入工程后，再做以下修改：

在DefaultEngine.ini的`[/Script/Engine.Engine]`下添加：

    +NetDriverDefinitions=(DefName="GameNetDriver",DriverClassName="OnlineSubsystemSteam.SteamNetDriver",DriverClassNameFallback="OnlineSubsystemUtils.IpNetDriver")

再增加：
    
    [OnlineSubsystem]
    DefaultPlatformService=Steam
     
    [OnlineSubsystemSteam]
    bEnabled=true
    SteamDevAppId=480

    [/Script/OnlineSubsystemSteam.SteamNetDriver]
    NetConnectionClassName="OnlineSubsystemSteam.SteamNetConnection"
    
然后启动编辑器后，以Standalone模式运行，且保证电脑上启动了Steam客户端，则启动游戏后会，在游戏屏幕右下角会自动弹出Steam相关菜单。

如果不使用该plugin，手动编写接入代码，则还需要添加以下配置：

+ 工程名.Build.cs构造函数中添加：

        PublicDependencyModuleNames.AddRange(new string[] { "OnlineSubsystem", "OnlineSubsystemUtils" });
        DynamicallyLoadedModuleNames.Add("OnlineSubsystemSteam");
  
+ 工程名.Target.cs构造函数中添加：

        bUsesSteam = true;

##### 手动接入steam SDK

Online Subsystem Steam  
https://docs.unrealengine.com/en-us/Programming/Online/Steam

Steam, Using the Steam SDK During Development  
https://wiki.unrealengine.com/Steam,_Using_the_Steam_SDK_During_Development

Integrating Steam SDK – Part 1  
http://orfeasel.com/steam_integration_p1/

Handling Steam Achievements – Steam Integration Part 2  
http://orfeasel.com/handling-steam-achievements-steam-integration-part-2/

中文翻译：  
集成 Steam SDK（一）  
http://gad.qq.com/program/translateview/7191581

处理Steam成就系统——接入Steam SDK（二）  
http://gad.qq.com/program/translateview/7191582

##### Shipping模式下steam集成无效的问题

在打包输出目录下，例如：\WindowsNoEditor\MyProj\Binaries\Win64\，新建一个文本文件：steam_appid.txt，并且内容为“480”。480表示steam测试使用的app id。

参考自：Steam integration not working on a Shipping Build  
https://answers.unrealengine.com/questions/474029/steam-integration-not-working-on-a-shipping-build.html

***
`人生没有彩排，每天都是直播。阳光，源自你内心的澄澈！`