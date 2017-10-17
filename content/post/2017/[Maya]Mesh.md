+++
title= "[Maya]Mesh"
date= "2017-10-02T12:01:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

##### Combine
假设有两个独立的物体，想把他们合并为一个整体。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-01.jpg">}}

先选中两个物体
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-02.jpg">}}

然后按住Shift + 鼠标右键，点击Combine
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-03.jpg">}}

这样两个物体就合并和一个整体，共享移动、伸缩、旋转等操作。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-04.jpg">}}

如果要分离两个物体，选中后按住Shift + 鼠标右键，点击Separate。

Combine和Separate的菜单位置再Mesh目录下：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-05.jpg">}}

##### Booleans
假设有两个物体相交在一起
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-06.jpg">}}

然后点击Mesh -》 Booleans，有三个选项：Union结合、Difference相减，Intersection相交。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-07.jpg">}}

+ Union 结合
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-08.jpg">}}

+ Difference 相减  
先选中的哪个物体，则保留哪个物体
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-09.jpg">}}

+ Intersection相交
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-10.jpg">}}


##### Triangulate和Quadrangulate（三角化/四角化）
假设有这样一个方框形状的模型，那么的某些面不是三角边也不是四角边
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-11.jpg">}}

如果需要将所有面转换为三角边或者四角边，点击：Mesh -》 Triangulate或者Quadrangulate
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-12.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-13.jpg">}}

##### Smooth
点击菜单Mesh -》Smooth，多次点击可多次平滑
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-14.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-15.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-16.jpg">}}

平滑的另外一种方式：
先按3预览平滑效果
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-17.jpg">}}

然后点击：Modify -》 Convert -》 Smooth mesh preview to polygons
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-18.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-19.jpg">}}

##### Mirror
假如有个模型，需要沿Y轴方向做对称处理
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-21.jpg">}}

点击Mesh -》 Mirror，选中Y轴，点击apply
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-22.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-23.jpg">}}

其中，镜像时控制顶点缝合的属性是Merge Threshold
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24.jpg">}}

##### Fill Hole
假设有这样一个模型，上面有个洞
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-25.jpg">}}
现在需要补洞，先选中洞的一条边（随便一条即可），然后点击Mesh -》 Fill Hole，或者按住shift键+鼠标右键 -》 Fill Hole，即可完成补洞。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-26.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-27.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-28.jpg">}}

##### Mesh Smooth
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-29.jpg">}}
一个正方体被Smooth之后的效果：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-30.jpg">}}

可以多次执行Smooth，执行次数越多则模型会圆滑：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-31.jpg">}}

