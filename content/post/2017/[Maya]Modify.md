+++
title= "[Maya]Modify"
date= "2017-10-02T18:06:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

##### 坐标轴相对物体居中
Modify -》Center Pivot
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-00.jpg">}}

##### NURBS转换为Polygon
点击菜单 Modify -》 Convert -》 NURBS To Polygons
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-01.jpg">}}

##### Universal Manipulator （快捷键：Ctrl + T，Q键取消）
用来显示物体的尺寸等信息
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-02.jpg">}}
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-03.jpg">}}

##### Math Transformations
假设有两个物体
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-04.jpg">}}

我们想将右边物体的Rotation复制到左边的物体上。方式如下：
先框选左边的物体，再按shift键框选右边的问题
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-05.jpg">}}

然后再点击Modify -》 Match Transformations -》 Math Rotation
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-06.jpg">}}
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-07.jpg">}}

##### Freeze Transformations
当物体执行Transform操作之后，Channel Box面板中的参数就会发生变化。例如：
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-08.jpg">}}
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-09.jpg">}}

如果此时就想以物体当前Transform为坐标轴的原点位置，Rotation也相当于初始时的Rotation，Scale也被当作为1，可以点击：Modify -》 Freeze Transformations。
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-10.jpg">}}

执行后，相关参数就会变化初始化的参数，但是物体的Transform不会变化。
{{< figure src="/img/20171002-[Maya]Modify/[Maya]Modify-11.jpg">}}

