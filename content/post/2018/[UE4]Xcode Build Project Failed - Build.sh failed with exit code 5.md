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
打开Launcher -》 Library -》 点击对应引擎版本下拉框 -》 Verify。然后继续编译Xcode工程（不用清理，如果清理重编，可能还会出现exit code 5的错误）

感觉是UE4的bug，出现这种问题的环境是：  
Mac OSX 10.13.3，Xcode 9.3，UE4.18 / 4.19

出现这个问题的原因，是因为我的UE4工程引用的第三方库没有对应的Mac版本（x86_64），所以每次一清理就出现exit code 5的错误，将工程所引用的所有第三方库都编译出对应的Mac版本，即可彻底解决此问题。xcode之前没用过，不知道其他C++工程对于缺少链接库的编译错误，是否都报exit code 5错误。

