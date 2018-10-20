+++
title= "[UE4]Montage Section切换无效的问题"
date= "2018-02-11T21:58:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

keywords: UE4 Montage Section not working

问题现象：  
SetNextSection在编辑器中运行正常，但是在打包版本中无效。

解决办法：  
将SetNextSection替换为JumpToSection。

参考自：Montage unwanted section switching  
https://answers.unrealengine.com/questions/172537/montage-unwanted-section-switching.html

{{< alert warning >}}
如果Section的时间很短，需要将 Blend In 和 Blend Out 设置为 改小或者设置为 0（默认为0.25），否则 JumpToSection 无效果。
{{< /alert >}}

***
`人生如逆旅，我亦是行人。----苏轼《临江仙》`