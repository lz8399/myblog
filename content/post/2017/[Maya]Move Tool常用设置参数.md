+++
title= "[Maya]Move Tool常用设置参数"
date= "2017-08-31T20:25:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++


双击Move Tool，打开参数菜单。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-01.jpg">}}

在Move Snap Settings下有个参数Retain Component Spacing，表示吸附操作时是否保持各个顶点的间距。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-02.jpg">}}

假设有这样两个平面物体，左下方的问题的某条边的4个顶点位置相互错开，现在要使用Snap to Points将这4个顶点吸附到右上角物体的边上。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-03.jpg">}}

开启Retain Component Spacing后效果：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-04.jpg">}}

关闭Retain Component Spacing后效果：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-05.jpg">}}

开启关闭Retain Component Spacing的快捷方式：W键按住不放+鼠标左键。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-06.jpg">}}

##### Soft Select 软选择（快捷键：B键）
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-07.jpg">}}

假设有个球体，选择了部分顶点，并准备移动这些顶点：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-08.jpg">}}

如果不开启Soft Select，那么想移动物体表面的某些顶点，效果是这样算的：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-09.jpg">}}

开启Soft Select之后，顶点的颜色会发生变化：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-10.jpg">}}

然后再移动，相比不开启的效果，模型的变化会比较自然。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-11.jpg">}}

如果要调节Soft Select的大小范围，按住B键不放，在拖拽鼠标左键：
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-12.jpg">}}

##### Soft Select的Falloff Mode
假设球体的某些面被删掉了
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-13.jpg">}}

如果Falloff mode为Volume，那么移动时，不会忽略被删掉的面，顶点会整体移动
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-14.jpg">}}
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-15.jpg">}}

如果Falloff mode选择Surface，则移动时会忽略断开的顶点。
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-16.jpg">}}
{{< figure src="/img/20170831-[Maya]Move Tool常用设置参数/[Maya]Move Tool常用设置参数-17.jpg">}}

<font color=red>注意：如果你的Soft Select范围太大，可能Surface和Volume两种模式没有效果，如果要使用Surface模式，需要将范围调整到尽量小的范围。</font>

***
`纵使相逢应不识，尘满面，鬓如霜。---苏轼《江城子》`
