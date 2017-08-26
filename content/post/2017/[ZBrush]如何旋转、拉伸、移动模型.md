---
title: "[ZBrush]如何旋转、拉伸、移动模型"
date: "2017-01-14T4:08:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords: ZBrush、Rotate、Scale、Move

##### Transpose控制线

**注意：<font color=red>要使用Transpose，必须将模型转换为PolyMesh3D。</font>**
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-07.jpg">}}


大多数3D软件，包括游戏引擎，都有提供物体的Transform操作：旋转(path，yaw，roll)，大小伸缩（scale）、位置移动（x、y、z）。这个功能4R8才提供，4R8之前的版本，要实现transform操作，使用的是Transpose，它是笔刷的个种类。具体用法是：
按下w键（或者点击菜单面板上Move图标），然后点击鼠标左键拖动，就可以拉出一根行动线，如果想让拉出的行动线与坐标轴保持平行或垂直，再按住shift键。
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-01.jpg">}}
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-02.jpg">}}

将鼠标悬停在黄色圆框内时，其内部会显示一个小圆框
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-03.jpg">}}

3个圆框均可以按住来拖拽，拖拽的作用分别是：

* 左边圆框是伸缩物体；
* 中间红框是移动物体；
* 左边红框是切削物体（比如把一个球切掉一半）；


##### 复制
在Transpose笔刷下，除了拖拽中间的圆圈来实现移动外，也可以使用按住Alt键、通过拖拽鼠标来移动物体。  
如果要复制一个物体，可以按住Ctrl键，然后鼠标按住中间的圆圈进行拖拽，来复制一个物体。

注意：<font color=red>复制的操作，必须是在删掉Lower Subdiv Level请的情况下，否则无法通过上面两种方式来移动和复制。</font>
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-04.jpg">}}


##### 移动
点击Transform –》 Move， 或者按W键
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-05.jpg">}}

然后拉出一条Transpose，再按住3个圆圈之一，进行拖拽，来实现不同方向上的移动。
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-06.jpg">}}

##### 伸缩
点击Transform –》 Scale，或者按E键

##### 旋转
点击Transform –》 Rotate，或者按R键

Transform的另外一种方式是，去掉Edit模式
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-08.jpg">}}

然后按住其中一个圆圈不放（一共三个，分别代表Pitch、Roll、Yaw），然后拖动鼠标或压感笔，就可以实现移动、伸缩或旋转。注意，当圆圈被选中时会变宽。
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-09.jpg">}}

注意：
<font color=red>移动、旋转、伸缩时一定要关闭Transform下面的对称，否则旋转就会出现变形。</font>
{{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-10.jpg">}}

##### Transpose控制线拉伸/伸缩
模型伸缩的规则，有两种方式：  

* Scale模式下的伸缩（快捷键E）  
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-11.jpg">}}

    假如在一个立方体模型的某一个面上，拉出一条从左到右（绿色圆圈和蓝色圆圈的那一头表示线条起点）的水平Transpose控制线。
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-12.jpg">}}

    然后按住中间的黄色圆圈，沿着控制线终点方向（红色箭头方向，此例子中的从左往右）拖动，那么当前面的上下两侧就会往外拉伸。
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-13.jpg">}}

    如果逆着控制线的方向，按住中间的黄色圆圈拖动，那么当前面的上下两侧就会往内压缩。
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-14.jpg">}}
    
    以正方体为例，这种模式下，控制线所在的一面的高度可以增加或减小，但是左右的两个面的长和宽会保持比例缩放
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-15.jpg">}}

* Move模式下的伸缩（快捷键W）  
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-16.jpg">}}
    
    Move模式下，是按住终点圆圈不放，然后左右移动鼠标，（如果想保持直线移动，可以按住shift键），来实现拉伸或缩短尺寸。移动的方向就是拉伸或者缩短的方向。
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-17.jpg">}}
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-18.jpg">}}
    
    如果想让模型某一端固定不变，让另一端自由伸缩甚至弯曲，可以先把鼠标悬停在右边圆圈后，然后按住Alt键不放，然后拖动鼠标。拖动鼠标过程中也可以同时按住shift键来保持直线移动。
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-19.jpg">}}
    {{< figure src="/img/20170114-[ZBrush]如何旋转、拉伸、移动模型/[ZBrush]如何旋转、拉伸、移动模型-20.jpg">}}
    