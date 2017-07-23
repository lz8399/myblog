---
title: "[ZBrush]Mirror镜像操作"
date: "2017-05-07T23:18:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

##### 反向镜像
点击：Tool -》 Deformation -》 Mirror，就可以将模型反向。
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-01.jpg">}}
Mirror按钮的右上角可以选择镜像基准轴向，可选的有X、Y、Z轴，默认是X轴。

执行前：
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-02.jpg">}}

执行后：
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-03.jpg">}}


##### 轴对称镜像
点击：Tool -》 Geometry -》 Modifier Topology -》 Mirror And Weld，可以将模型左边的部分复制模型右边。
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-04.jpg">}}
按钮的右上角可以选择镜像基准轴向，可选的有X、Y、Z轴，默认是X轴。

执行前：
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-05.jpg">}}

执行后：
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-06.jpg">}}

##### 如何判定模型的X、Y、Z方向
比如要镜像模型时，如何判断当前模型的朝向。可以按下W键或E键，并保证当前模型是PolyMesh3D，就可以看到Transform线条，红、绿、蓝三种颜色，分别代表X、Y、Z轴。
{{< figure src="/img/20170507-[ZBrush]Mirror镜像操作/[ZBrush]Mirror镜像操作-07.jpg">}}