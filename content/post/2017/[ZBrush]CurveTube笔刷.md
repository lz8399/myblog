---
title: "[ZBrush]CurveTube笔刷"
date: "2017-04-16T23:34:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-01.jpg">}}

##### 曲线大小
控制曲线大小的是笔刷的Draw Size
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-02.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-03.jpg">}}


如果修改曲线的粗细，调整Draw Size之后，点击下斑马线即可：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-04.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-05.jpg">}}

##### 曲线斑马线使用
CurveTube笔刷可以拉出一条管道装的模型。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-06.jpg">}}

拉出来以后，管道中间会有一条斑马线。可以按住斑马线的中间或者两端拖拽：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-07.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-08.jpg">}}


如果确定管道的形状后不需要继续编辑了，那么可以点击下管道以外的其他模型的位置，此时斑马线就会消失：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-09.jpg">}}

删除斑马线另外一种方式：Stroke -》 Curve Functions -》 Delete
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-10.jpg">}}

##### Smooth（曲线平滑）
编辑曲线过程中，如果曲线不够圆滑了：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-11.jpg">}}

可以点击 Stroke -》 Curve Functions -》 Smooth。可以点击多次，越点击越圆滑：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-12.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-13.jpg">}}

等达到预期效果后，再点击一下斑马线，就可以让曲线变圆滑：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-14.jpg">}}


##### 曲线吸附模型表面
编辑曲线管道时，曲线的默认走向是不会贴着模型表面的，如果想让曲线在拉伸的过程中贴着模型表面，点击：菜单栏 -》 Picker -》 Cont Z。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-15.jpg">}}

这样拉出的曲线就会吸附在模型的表面上（粉色的曲线为打开Cont Z后的效果，绿色的曲线为Once Z的效果）：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-16.jpg">}}

##### Curve Modifiers使用
菜单栏-》Stroke，即可打开CurveTube笔刷的编辑面板：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-17.jpg">}}

点击Stroke -》 Curve Modifiers -》 Size，可以让曲线有粗细渐变。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-18.jpg">}}

比如假设启用Size之前，曲线的形状是这样的：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-19.jpg">}}

启用Size之后，再点击下斑马线：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-20.jpg">}}


曲线渐变的节奏可以在曲线编辑器中控制
单击Stroke -》 Curve Modifiers -》 Curve Falloff，即可打开曲线编辑面板：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-21.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-22.jpg">}}


如果想让曲线中间粗，两端细，那么可以在曲线编辑器中调整为：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-23.jpg">}}

这样画出来的曲线效果为：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-24.jpg">}}

#####设置曲线横截面的边的条数
Brush -》 Modifiers -》 Brush Modifier，比如修改为4，那么曲线的横截面的边的条数只有4条，画出来的曲线相当于一个立方体。这个数值越大，则曲线的横截面越接近圆形。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-25.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-26.jpg">}}

设置Brush Modifier之后的效果，和CurveTubeSnap笔刷的效果类似，该笔刷的Brush Modifier值默认为8：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-27.jpg">}}


##### 设置曲线的纵向密度
值越小，表示纵向的密度越大：
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-28.jpg">}}

例如，上边曲线的密度为0.1，下边曲线的密度为0.8
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-29.jpg">}}

设置端点自动吸附的距离
当光标离斑马线的断点较近时，会自动出现一条红线，此时按住鼠标或压感笔，可以接着当前的位置继续画曲线。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-30.jpg">}}

如果想修改默认的自动吸附距离，修改：Stroke -》 Curve Modifiers -》 Curve Snap Distance。
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-31.jpg">}}

比如在做毛发时，头发比较密集，如果Curve Snap Distance设为0，则新画的曲线不会自动连接旧的曲线。

##### ZRemesherGuides使用
CurveTube笔刷是每画一条斑马线，曲线就会立即出现；而ZRemesherGuides可以先多次间断的编辑斑马线，等编辑后之后，在生成曲线。
1，先切换到ZRemesher笔刷
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-32.jpg">}}

2，然后我们可以先多次间断的编辑斑马线
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-33.jpg">}}
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-34.jpg">}}

3，编辑好之后，再切换到CurveTube笔刷，然后点击下斑马线，即可生成曲线
{{< figure src="/img/20170416-[ZBrush]CurveTube笔刷/[ZBrush]CurveTube笔刷-35.jpg">}}
