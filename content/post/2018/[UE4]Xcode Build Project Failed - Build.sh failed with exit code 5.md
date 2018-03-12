+++
title= "[UE4]Xcode Build Project Failed - Build.sh failed with exit code 5"
date= "2018-03-12T22:08:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Mac", "Generate Xcode Project File"]
+++

生成Xcode project file之后，打开Xcode并编译运行（Cmd + R ），提示以下错误:

    Command /Users/Shared/EpicGames/UE_4.18/Engine/Build/BatchFiles/Mac/Build.sh failed with exit code 5
    
解决办法：  
打开Launcher -》 Library -》 点击对应引擎版本下拉框 -》 Verify。

感觉是UE4的bug，出现这种问题的环境是：  
Mac OSX 10.13.3，Xcode 9.3，UE4.18/4.19