---
title: "[ZBrush]使用蒙板掏空挖洞"
date: "2017-04-13T23:14:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords： Mask、MaskPen、DynaMesh、掏空、挖洞

注意，开始之前记得将模型转换为DynaMesh：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-01.jpg">}}

这里演示掏空一个圆柱，所以我们可以使用InsertCylinder笔刷：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-02.jpg">}}

按住Alt键（相当于反向操作），在一个面板上拉出一个圆柱。默认圆柱只有单面：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-03.jpg">}}

再点击Tool -》 Display Properties -》 Double，就可以看到双面：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-04.jpg">}}
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-05.jpg">}}

在空白区域拖拽一下鼠标左键，取消蒙板：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-06.jpg">}}

然后在空白区域点击鼠标左键，全体覆盖蒙板
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-07.jpg">}}

然后再拖拽一下鼠标左键，取消所有蒙板：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-08.jpg">}}

最后再拖拽一下鼠标左键，执行Re-DynaMesh，让圆柱消失：
{{< figure src="/img/20170413-[ZBrush]使用蒙板掏空挖洞/[ZBrush]使用蒙板掏空挖洞-09.jpg">}}