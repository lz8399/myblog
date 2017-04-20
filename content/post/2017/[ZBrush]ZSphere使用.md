---
title: "[ZBrush]ZSphere使用"
date: "2017-01-17T23:30:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

#### Z球使用步骤
新建Z球：
Tool -》 Tool -》 ZSphere
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-01.jpg">}}

新建后默认是Draw模式（快捷键Q），这个模式下只能新建z球的节点：
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-02.jpg">}}

如果想拉伸两个节点之间的距离，需要切换到Move模式下（快捷键W）
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-03.jpg">}}

打开Tool -》 Unified Skin -》 Preview（快捷键A）可以打开和关闭预览，如果觉得预览的分辨率太低，可以增大Resolution参数来预览高分级别的效果。
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-04.jpg">}}
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-05.jpg">}}


如果打开Tool -》 Sketch -》 EditSketch（快捷键Shift + A），则会切换到另外一种状态，且此时的笔刷变成了Sketch
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-06.jpg">}}

如果用Sketch笔刷画，则会产生像泥条一样的形状。
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-07.jpg">}}
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-08.jpg">}}

这个功能的作用是：先给模型建立骨骼，然后在骨骼上途泥条建立肌肉，之后就可以移动骨骼的同时来移动肌肉。如果想还原到Z球状态，在按下Shift + A。

#### EditSketch
打开Tool -》 Sketch，取消EditSketch之后，就可以以X光显示出之前的Z球骨架
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-09.jpg">}}
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-10.jpg">}}

此时再切换到Z球的Move模式下，并选中Sketch下的Bind，就可以调整再次调整骨架，此时Z球上的泥条，也会跟着一起移动。
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-11.jpg">}}
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-12.jpg">}}

这个功能可以很方便的来调整造型，因为只需要移动骨架就可以让表面形状一起移动。

在EditSketch模式下，再点击预览Adaptive Skin（快捷键也是A），则会显示模型的低分级别（Lower Subdiv Resolution）效果
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-13.jpg">}}
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-14.jpg">}}


#### 注意事项：
1，在途泥条的时候，可以经常点击Optimize来优化泥条的覆盖问题：可以自动删除掉泥条堆叠时的被覆盖掉的部分。
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-15.jpg">}}

2，途泥条时，如果想抹掉一部分，可以按住Alt键+鼠标左键。注意，涂抹泥条或擦掉泥条时，笔刷模式一定要是Draw模式，Z球移动时的Move模式无法修改泥条。
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-16.jpg">}}

3，Z球转换PolyMesh3D
在Preview模式下（Unified Skin或Adaptive Skin下的Preview），点击Make PolyMesh3D，就可以创建一个PolyMesh对象
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-17.jpg">}}

然后再点击Tool -》 Geometry -》 Higher Res（快捷键D），就可以获得高分级别的模型
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-18.jpg">}}

如果觉得细分还不够高，可以再点击Divide（快捷键Ctrl + D）
{{< figure src="/img/20170117-[ZBrush]ZSphere使用/[ZBrush]ZSphere使用-19.jpg">}}