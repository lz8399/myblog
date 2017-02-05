---
title: "[UE4]UE_LOG在Android版本(LogCat)中开启的注意事项"
date: "2016-10-16T01:40:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---


比如UE4工程的C++代码中有如下log打印语句：

    UE_LOG(LogTemp, Display, TEXT("aaaaaaa"));

我们希望这句话在Android Device Monitor中能也能够打印出来，需要在将设备的Config设置为DebugGame或者Development，Shipping下则不会打印。

{{< figure src="/img/20161016-[UE4]UE_LOG在Android版本(LogCat)中开启的注意事项.jpg">}}

