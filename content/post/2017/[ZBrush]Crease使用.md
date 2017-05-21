---
title: "[ZBrush]Crease使用"
date: "2017-04-23T11:37:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Tool -》 Geometry -》 Crease -》 Crease
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-01.jpg">}}
##### 作用：
当执行平滑或者细分时，希望模型局部位置的细节不被平滑掉，则可以使用Crease。

##### 用法：
1，先用套索选出需要被保护的细节部分：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-02.jpg">}}
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-03.jpg">}}


然后点击CreaseAll，表示对选中部分的所有Mesh网格保护，如果点击Crease，那么只对边沿做保护。
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-04.jpg">}}
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-05.jpg">}}


然后执行细分：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-06.jpg">}}

最终效果：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-07.jpg">}}

##### CreaseCurve
另外有个专门做Crease曲线的笔刷。选中后，再按住Ctrl + Shift不放，即可使用该笔刷
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-08.jpg">}}

按住鼠标不放，即可开始编辑曲线，默认是直线，如果需要转弯，按一下Alt键并松开，即可让曲线转弯：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-09.jpg">}}

如果转弯角度不需要圆滑，而是两个直线夹角，则在编辑过程中（Ctrl + Shift）连续按两次Alt键，即可让线条以直线线段来编辑：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-10.jpg">}}

当松开鼠标时，即可完成编辑：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-11.jpg">}}

然后再执行细分：
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-12.jpg">}}

细分后，之前编辑的CreaseCurve位置，就不会被平滑掉。
{{< figure src="/img/20170423-[ZBrush]Crease使用/[ZBrush]Crease使用-13.jpg">}}

其他资料：  
http://www.zbrushcn.com/jinjie/ruhe-kabian.html
