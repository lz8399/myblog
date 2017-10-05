+++
title= "[Maya]Merge Vertices和Target Weld的区别"
date= "2017-10-03T00:23:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

Merge Vertices表示将多个顶点合并为一个点，且这个新的顶点的位置可能不是原有顶点的位置。
Target Weld 也是多个点合并为一个点，但是每次只能同时合并两个，且合并过程中需要手动指定起始顶点和目标顶点，而Merge Vertices则不用关心起始顶点和目标顶点。

以下面的模型为例
{{< figure src="/img/20171003-[Maya]Merge Vertices和Target Weld的区别/[Maya]Merge Vertices和Target Weld的区别-01.jpg">}}

两种效果分别为：  
Merge Vertices（合并点的间隔可以设置，这里为了演示将Threshold设置了最大，即合并为一个点）
{{< figure src="/img/20171003-[Maya]Merge Vertices和Target Weld的区别/[Maya]Merge Vertices和Target Weld的区别-02.jpg">}}

Target Weld
{{< figure src="/img/20171003-[Maya]Merge Vertices和Target Weld的区别/[Maya]Merge Vertices和Target Weld的区别-03.jpg">}}

Merge Vertices和Target Weld快捷键：按住Shift+鼠标右键-》Merge Vertices。
{{< figure src="/img/20171003-[Maya]Merge Vertices和Target Weld的区别/[Maya]Merge Vertices和Target Weld的区别-04.jpg">}}
{{< figure src="/img/20171003-[Maya]Merge Vertices和Target Weld的区别/[Maya]Merge Vertices和Target Weld的区别-05.jpg">}}


参考：  
Merge Vertices and Target Weld in Maya
https://www.youtube.com/watch?v=LsDnWZ4hHTk
