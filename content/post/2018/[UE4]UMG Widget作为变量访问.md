+++
title= "[UE4]UMG Widget作为变量访问"
date= "2018-04-01T13:47:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Widget Blueprint"]
+++

默认情况下，UMG蓝图钟的Widget组件只能在当前UMG蓝图钟访问，无法在外部被其他蓝图访问。  
如果要被外部访问，方式如下：

设计面板（Designer）中勾选Is Variable

{{< figure src="/img/20180401-[UE4]UMG Widget作为变量访问/[UE4]UMG Widget作为变量访问-01.jpg">}}
{{< figure src="/img/20180401-[UE4]UMG Widget作为变量访问/[UE4]UMG Widget作为变量访问-02.jpg">}}
