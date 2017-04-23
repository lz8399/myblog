---
title: "[ZBrush]DynaMesh使用"
date: "2017-03-05T21:34:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

#### 启用DynaMesh的步骤
1，先删除模型的低细分级别：Tool -》 Geometry -》Del Lower
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-01.jpg">}}
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-02.jpg">}}

2，然后点击Tool -》 Geometry -》 DynaMesh -》 DynaMesh
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-03.jpg">}}

DynaMesh之前，Resolution的值为多少，则分辨率就是多少。比如上图中，Resolution为128。

#### Re-DynaMesh的步骤

注意：执行Re-DynaMesh的前提是已经启用了DynaMesh，即”DynaMesh”按钮是选中状态。
1，假设下图是原始mesh的分辨率为128，我们准备将其Re-DynaMesh为分辨率为32的mesh。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-04.jpg">}}

2，现在Resolution调整为32，并增加一次Divide。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-05.jpg">}}

3，然后在空白区域，按住鼠标左键拖拽一下，就可以执行Re-DynaMesh。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-06.jpg">}}

另外一种Re-DynaMesh方式：
在上面的第2步之后，点击Del Lower
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-07.jpg">}}

然后再点击DynaMesh两次：相当于重新关闭和打开DynaMesh
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-08.jpg">}}

#### DynaMesh的4个参数作用
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-09.jpg">}}

* `Groups`：如果mesh有多个分组，点击此按钮可以让分组之前的界限更明显；
* `Polish`：让物体表面更平滑；
* `Blur`：Project按钮启用时生效，值越多，模糊掉的细节越多，值越小，模糊掉的细节越少；
* `Project`：重新绘制Mesh网格，比如当你的mesh网格拉伸扭曲了，可以通过此按钮将表面重新恢复均匀；如果想让两个Group合并编辑（两个不同Group在没有合并的情况下，同时编辑），也需要打开Project并执行Re-DynaMesh。

### Freeze SubDivision Levels的意义
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-10.jpg">}}

#### 意义1：MeshInsert Dot Brush
启用Freeze SubDivision Levels的用途之一：当使用MeshInsert Dot Brush笔刷时，可以锁住之前模型的细分级别，这样可以让新建的模型和老的模型分别已不同的细分级别同时共存。
例如下图中，启用Freeze SubDivision Levels后，在圆球上见两个突起物；红球的分辨率为32，两个突起部位的分辨率为128，此时两种分辨率同时共存。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-11.jpg">}}

MeshInsert Dot Brush使用完毕以后，然后关闭Freeze SubDivision Levels，此时会将所有mesh的分辨率调整为最高的分辨率。当前所有mesh中，分辨率最高的32，所以关闭Freeze SubDivision Levels后，所有mesh的分辨率编程了128。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-12.jpg">}}

启用和关闭Freeze SubDivision Levels，可以来实现高分和低分mesh的来回切换：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-13.jpg">}}
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-14.jpg">}}


#### 意义2：DynaMesh编辑
在Freeze SubDivision Levels启用后，DynaMesh模式下编辑模型：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-15.jpg">}}

编辑完毕后再关闭Freeze SubDivision Levels，就可以将Freeze SubDivision Levels启用时编的部分以不同的细分级别显示出来。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-16.jpg">}}


#### Resolution的意义
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-17.jpg">}}
1，Resolution的值为多少，那么mesh首次转换为DynaMesh后的默认分辨率就是多少。
2，Re-DynaMesh（重新拓扑）的时候，mesh新的分辨率就是当前Resolution的值。


#### Re-DynaMesh的实际应用
##### 1，网格重新拓扑
当模型网格被拉坏以后，比如这样：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-18.jpg">}}

如果想让这些被拉坏的网格重新平均排布（Re-DynaMesh），方式如下：
先选中Tool -》 Geometry –》 DynaMesh -》Projected，然后再点击：Tool -》 Geometry –》 DynaMesh -》DynaMesh
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-19.jpg">}}

再按住Ctrl键，在空白地方按住鼠标左键不放拖拽一下：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-20.jpg">}}

这样变形的网格就会重新分布
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-21.jpg">}}

也可以关闭DynaMesh再启用DynaMesh（双击两次，启用前需要Del Lower），通过切换状态来实现网格重新拓扑：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-22.jpg">}}

##### 2，合并编辑两个Group。
两个PolyGroup，默认是只能同时编辑一个的，就是说笔刷刷上去，默认只对一个Group有效：
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-23.jpg">}}
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-24.jpg">}}

如果想让笔刷同时对两个Group有效且两个Group不合并，那么就可以就可以按上面的例子一样，打开Project之后在执行Re-DynaMesh，这样就可以同时编辑两个Group。
{{< figure src="/img/20170305-[ZBrush]DynaMesh使用/[ZBrush]DynaMesh使用-25.jpg">}}
 

