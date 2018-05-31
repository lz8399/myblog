---
title: "[ZBrush]Project All实例(example)"
date: "2017-04-16T22:26:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords：ZBrush, Project All, Mask, 布线, 投射


Project All实际应用：
我们假设有一个布线过的高分模型，但是局部的布线有问题，我们想只对这些局部的重新拓扑，这时就可以使用Project All功能。

步骤：  
1，假设存在一个高分模型，Resolution为128，此时在SubTool中复制一个：
Tool -》 SubTool -》Duplicate
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-01.jpg">}}

2，复制之后，在对复制出的模型执行Re-DynaMesh（Tool -》 Geometry -》 DynaMesh -》 DynaMesh），并将Resolution设低一点，比如16；然后再对该模型进行多次Divide（Tool -》 Geometry -》 Divide）；Divide之后，再讲该模型的细分级别设置为低细分级别（修改Tool -》 Geometry -》 SDiv），这里假设SDiv为2：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-02.jpg">}}

3，假设此时上面模型的Resolution别为128，下面模型的Resolution为16（SDiv为2）：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-03.jpg">}}
则此时高分模型和低分模型的形体会产生差异：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-04.jpg">}}

然后执行：Tool -》 SubTool -》Project -》 Project All：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-05.jpg">}}
注意：执行前将Project参数Dist设为1。

执行Project All之后，ZB就会自动帮你将高分模型和低分模型之间的差异中和掉：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-06.jpg">}}

此时再隐藏掉高分模型，就可以只对低分模型重新布线：
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-07.jpg">}}
{{< figure src="/img/20170416-[ZBrush]Project All实例(example)/[ZBrush]Project All实例(example)-08.jpg">}}

***
`唉，奴隶般的意大利，你哀痛之逆旅，你这暴风雨中没有舵手的孤舟，你不再是各省的主妇，而是妓院！---《神曲》`