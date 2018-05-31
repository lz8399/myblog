---
title: "[ZBrush]SubTool使用(类似PS的Layer)"
date: "2017-04-13T00:12:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords：挤出、Extract、合并、Merge、掏空、挖洞

#### Extract（挤出）
现在模型上画一个mask（按住Ctrl+鼠标左键）
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-01.jpg">}}

然后点击Tool -》 SubTool -》 Extract -》 Extract，点击后只是预览效果，如果确认，再点击Accept
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-02.jpg">}}
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-03.jpg">}}


#### Merge（合并）
假设场景中已经有一个球体。
1，点击Tool -》 SubTool -》Append -》选择一个正方体
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-04.jpg">}}
将新建出来的正方体移动到一个合适的位置
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-05.jpg">}}

2，选中第一个SubTool，然后点击下方的Merge -》 MergeDown
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-06.jpg">}}

最终效果：
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-07.jpg">}}

然后再执行DynaMesh，就可以将两个SubTool的交界处进行融合：
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-08.jpg">}}

合并之后，两个subtool仍然可以独立编辑。比如将Brush -》 Auto Masking -》 Mask By PolyGroups改为100，然后就可以只编辑其中一个。因为Merge之后还是两个单独的group，所以两个group可以独立编辑
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-09.jpg">}}

#### 使用SubTool挖洞（掏空）
1，新建一个圆柱体的SubTool，插入正方体里面。
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-10.jpg">}}

2，在SubTool继续选中这个圆柱体，再点击：Tool -》 PolyGroups -》 Group As DynaMesh Sub -》
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-11.jpg">}}

点击后的效果：
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-12.jpg">}}

3，选中SubTool中圆柱体的“相减”的bool运算符
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-13.jpg">}}

4，选中正方体，并执行MergeDown
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-14.jpg">}}

执行后的效果：
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-15.jpg">}}


5，最后再Re-DynaMesh一下。由于之前没有转换为DynaMesh，所以这里转换为DynaMesh。
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-16.jpg">}}

转换为DynaMesh后，圆柱体会自动消失，并掏空正方体，最终效果：
{{< figure src="/img/20170413[ZBrush]SubTool使用(类似PS的Layer)/[ZBrush]SubTool使用(类似PS的Layer)-17.jpg">}}

***
`当然，行是行的，这固然很好，可是千万别闹出什么乱子来啊。---《套中人》`