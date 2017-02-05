+++
title= "[UE4]如何获取FString转换后char之后的长度"
date= "2016-09-10T17:15:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

比如用TCHAR_TO_ANSI()将tchar转换为char之后，char的长度如何计算？
使用FTCHARToANSI::Length()，示例如下：

    FTCHARToANSI Convert(*String);
    Ar->Serialize((ANSICHAR*)Convert, Convert.Length());

参考自：https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/StringHandling/CharacterEncoding/index.html
