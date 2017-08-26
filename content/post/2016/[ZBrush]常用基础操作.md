---
title: "[ZBrush]常用基础操作"
date: "2016-11-26T21:28:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

##### 打开默认的空白界面：
点击左上角的“LightBox”，再选择一个默认模型。

##### 替换掉当前的物体，新建一个默认模型
Tool -》 Tool。类似Max的参数化物体，可以快速新建一个基础形状的物体。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-01.jpg">}}
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-02.jpg">}}

##### 笔刷的3个基础属性：
* Z Intensity：Z强度，这个用鼠标不是很敏感，如果用数位板，笔刷的力度会根据压感笔的力度变化。以Zadd笔刷为例，Z强度越大，则笔刷隆起的高度越高；
* Focal shift：笔触大小/焦点衰减，值越大，则笔刷的焦点越集中，值越小，则笔刷的焦点越分散，但集中和最大分散范围不会超过DrawSize笔刷大小的尺寸。
例子，上、中、下笔刷效果分别对应笔触为-70、0、70的效果：
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-03.jpg">}}
* Draw Size：笔刷大小；这个很好理解，就是笔刷的尺寸，类似毛笔的小楷和大楷的尺寸区别


##### 设置模型分辨率
点击Tools -》 Geometry，默认的模型分辨率级别为3，如果要调整，拖动SDiv滑动条来扩大和缩小分辨率级别。
可以点击和Lower Res和Higher Res来切换高高低分辨率；点击Divide（分裂）扩大模型的网格数量，每点击一次，网格数量则增加4倍。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-04.jpg">}}

注意：要修改分辨率，必须将模型转换为PolyMesh3D，否则找不到Resolution的相关按钮。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-05.jpg">}}


##### 绘制直线时如何让线条更笔直（减少抖动）：
将Mouse Avg设置大点，提高鼠标的灵敏度
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-06.jpg">}}

也可以使用Stroke下面的Lazy Mouse：
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-07.jpg">}}

##### 使用Layer：
展开Layers面板，点击右下角的加号按钮，这样就可以新建一个Layer。类似PS的图层。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-08.jpg">}}

##### 笔刷的相对大小设置：
按住shift不放，然后在鼠标单击Dynamic。当启用Dynamic之后，笔刷大小会随着视角拉伸自动缩放，如果不启用，则无论怎么拉伸角度，笔刷大小都不会变化。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-09.jpg">}}


##### 保存文件
保存文件有两种方式，一种时保存整个zbrush的工作环境文件，包括历史记录和zb当前的软件参数设置等；一种是保存当前zbrush的对象文件，没有历史和zb配置信息。
保存带工作环境的工程文件*.ZPR：
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-10.jpg">}}

只保存模型对象文件*.ztl：
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-11.jpg">}}

##### 关闭对称
Transform –》Activate Symmetry，取消选中X轴。如果点选X轴，则是对称雕刻。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-12.jpg">}}


##### 撤销工具栏
在zb上方，有个横向的滑动条，你的雕刻次数越多，这个滑动条越来越长，拖动或点击时，当前雕刻的物体可以回退到之前的状态。这样方便快速撤销到之前的某个时间段的状态。
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-13.jpg">}}


##### 法线双面显示
默认的法线只显示一面，如果要正反都显示：点击Tool -》 Display Properties -》Double
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-14.jpg">}}
Flip表示法线反转：之前隐藏的面进行显示，之前显示的面隐藏掉。

##### 模型导入导出
导出ZTL
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-15.jpg">}}

导出OBJ
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-16.jpg">}}

导出ZPR
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-17.jpg">}}

导入ZTL
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-18.jpg">}}

导入OBJ
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-19.jpg">}}

导入ZPR
{{< figure src="/img/20161126-[ZBrush]常用基础操作/[Zbrush]常用基础操作-20.jpg">}}

注意：<font color=red>如果是刚启动ZB之后，从空白场景导入、在场景中用鼠标拉导入的模型后，默认是不可编辑的，如果想让模型继续编辑，按T键。</font> 
如果场景已有现成的模型，这个时候再导入新模型时，是可以不用按T，直接可以编辑的。

