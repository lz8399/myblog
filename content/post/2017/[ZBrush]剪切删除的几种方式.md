---
title: "[ZBrush]剪切删除的几种方式"
date: "2017-05-07T20:33:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords：ZBrush、Delete、Clip、Hide、Close Hole

##### 使用SelectRect笔刷

1，先点击一下SelectRect笔刷：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-01.jpg">}}

然后就会提示你按住Ctrl + Shift来使用，点击OK。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-02.jpg">}}

2，然后按住Ctrl + Shift，就可以直接启用刚刚点击的SelectRect笔刷。另外笔刷的Stroke类型建议选择Lasso，它可以选择不规则形状的模型部位。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-03.jpg">}}

如果使用过一次后，那么再次按住Ctrl + Shift键，然后点击下Brush，就可以看到历史记录了，然后点击一下就可以选中SelectRect笔刷。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-04.jpg">}}

3，按住Ctrl + Shift，然后按住鼠标不放，用套索选择要剪切的部位：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-05.jpg">}}

剪切之后，就只能看到用套索选中的部位，其他部分被隐藏了。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-06.jpg">}}

如果想反向显示没有被选中的部位，则按住Ctrl + Shift，然后在空白区域拖拽一下鼠标即可：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-07.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-08.jpg">}}

如果在空白区域不拖拽，只是点击一下，那么模型将还原到剪切前的状态。

4，圈好需要保留的部分后，再点击Tool-》 Geometry -》 Modify Topology -》 Del Hidden：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-09.jpg">}}

5，然后在执行Re-DynaMesh（<font color=red>假设你提前已启用DynaMesh了</font>）：在空白区域拖延一下鼠标：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-10.jpg">}}

最后，之前隐藏的部分就被剪切删除了。被剪切掉的空白区域，就会自动被填充一层。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-11.jpg">}}

这里除了可以通过执行Re-DynaMesh来填充空洞的区域，还可以通过点击：Tool-》 Geometry -》 Modify Topology -》 Close Holes。两种方式都需要执行Del Hidden，即第4步都要执行，只是第5步有区别。
注意事项：<font color=red>如果使用Close Holes，则可以不启用DynaMesh。</font>
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-12.jpg">}}

最后补充：按住Ctrl + Shift是选中显示的部位，其余部分隐藏掉；按住Ctrl + Shift + Alt正好相反。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-13.jpg">}}

##### 使用ClipRect笔刷
这里我们使用zb自带的一个齿轮模型来演示：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-14.jpg">}}

1，用相同方式选中ClipRect笔刷：先点击ClipRect，然后再按住Ctrl + Shift：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-15.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-16.jpg">}}

2，然后再按住鼠标不放，选中我们要保留的区域：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-17.jpg">}}

3，这样就可以一步到位实现剪切删除：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-18.jpg">}}

但这样剪切的出来的模型的布线有问题：剪切后的截面，布线很乱，因为ClipRect笔刷做的操作是将待删除的部分压扁，所以被删除部分的布线还遗留在模型上。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-19.jpg">}}

<font color=red>针对这种非常不规则的模型，剪切删除时最好使用TrimLasso，用其剪切删除的界面，不会遗留不干净的布线。</font>

##### 使用TrimLasso笔刷
1，用相同方式选中TrimLasso笔刷：先点击TrimLasso，然后再按住Ctrl + Shift：
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-20.jpg">}}

2，使用TrimLasso前，模型必须转换为PolyMesh3D。另外一个区别是：ClipRect选中的区域会保留下来，而TrimLasso选中的区域会被删除。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-21.jpg">}}

3，选中后，保留下来的部分的截面，其布线是非常均匀的，没有所形状影响。
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-22.jpg">}}

ClipRect和TrimLasso一个区别是：<font color=red>使用前者时不需要转换为PolyMesh3D，而使用后者时需要转换为PolyMesh3D。</font>

##### 使用Lasso的注意事项
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-23.jpg">}}

Lasso有两种款选模式，一种是逆时针，一种顺时针。  
<font color=red>逆时针框选表示删除款选的部分；顺时针表示删除框选以外的部分。</font>

* 逆时针  
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-24.jpg">}}
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-25.jpg">}}

* 顺时针  
    注意，顺时针时，起点和终点分别要越过模型下方边界和上方边界
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-26.jpg">}}
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-27.jpg">}}

    如果没有超过模型的上下边界，则剪切效果有乱掉。因为顺时针时，剪切操作相当于：以起点和终点的连接为平面，将框选之外的部分压扁到该平面上，所以若起点和终点没有覆盖模型的上下边界，模型的上下部位在压扁过程中会漏掉。
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-28.jpg">}}
    {{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-29.jpg">}}
    
使用Curve的方式与Lasso类似，由于直线没有顺时针逆时针的概念，所以zb用黑色阴影标识哪一遍被删除：<font color=red>直线有阴影的一边会被删除，没有阴影的一边会被保留。</font>
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-30.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-31.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-32.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-33.jpg">}}
{{< figure src="/img/20170507-[ZBrush]剪切删除的几种方式/[ZBrush]剪切删除的几种方式-34.jpg">}}
