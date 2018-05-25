+++
title= "[Maya]Mesh Display"
date= "2017-10-17T13:25:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya Normal Reverse"]
+++

Maya版本为2018
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-01.jpg">}}

##### Reverse 法线反转
默认情况下，场景灯光没有开启双面显示
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-02.jpg">}}

那么法线反方向的面会显示为黑色
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-03.jpg">}}

如果希望将这些黑色面的法线方向反转，选中面以后，点击：Mesh Display -》 Reverse。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-04.jpg">}}
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-05.jpg">}}

Reverse的Hotbox为：按住Shift+鼠标右键 -》 Face Normals -》 Reverse Normals。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-06.jpg">}}
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-07.jpg">}}

##### Lock Normals 锁定法线
假如有个正方体，硬边时的顶点法线如下：
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-08.jpg">}}
改为软边后的顶点法线如下：
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-09.jpg">}}
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-10.jpg">}}

改成软边后，然后再压扁物体，顶点法线的方向也会随关联的面的面积变化而变化。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-11.jpg">}}

如果在压扁过程中希望顶点法线保持原有的方向，则可以在压扁之前固定法线：Mesh Display -》 Lock Normals。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-12.jpg">}}

固定法线之后，法线颜色就变成了黄色
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-13.jpg">}}

然后再压扁时，顶点法线的方向不会变化。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-14.jpg">}}

##### Average Normals 平均法线
对于这种硬边结构
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-15.jpg">}}

如果改成软边，则顶点法线的方向不会按照关联的3个面的法线方向进行平均处理：
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-16.jpg">}}

如果想让顶点法线方向不受面的大小影响，只受面的法线方向影响，则可以执行Average平均法线：Mesh Display -》 Average。执行Average之后，被选中的部分会被转换为软边。
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-17.jpg">}}
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-18.jpg">}}

如果只选中部分，那么该部分进行法线平均
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-19.jpg">}}
{{< figure src="/img/20171017-[Maya]Mesh Display/[Maya]Mesh Display-20.jpg">}}

{{< alert danger >}}
注意：法线平均时只对硬边有效，对软边无效。
{{< /alert >}}

***
`君子交绝，不出恶声。---《战国策》`