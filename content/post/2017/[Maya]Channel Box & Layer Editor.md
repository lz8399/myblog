+++
title= "[Maya]Channel Box & Layer Editor"
date= "2017-11-14T15:09:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya", "Layer"]
+++

Maya版本为2018


打开Channel Box/Layer Editor的按钮：
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-01.jpg">}}
或者点击：Windows -》 General Editors -》 Channel Box/Layer Editor。
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-01-01.jpg">}}
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-02.jpg">}}

##### Layers
在Display面板下，点击右上角的按钮：Create a new layer.
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-03.jpg">}}
然后双击layer，可以修改相关属性
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-04.jpg">}}

+ Name：层的名字
+ Display type：有三种，Normal、Template、Reference，对应Layer显示栏的第3个方框，空白表示Normal。
+ Visible：是否可见，对应Layer显示栏的第1个方框，默认为显示，即第一个方框显示为“V”。
+ Hide on playback：是否在播放动画的时候隐藏当前layer。对应Layer显示栏的第二个方框，默认为P，表示参与播放动画，不隐藏。
+ Color：表示Layer的标识颜色，对应Layer显示栏的第4个方框，默认没有颜色。


新建好一个Layer之后，在选中需要加入当前layer中的对象，
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-05.jpg">}}

然后右键点击layer -》 Add Selected Objects。这样之后就可以通过控制当前layer的显示，来控制在当前layer下的所有物体的显示。
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-06.jpg">}}

##### Layer显示栏的4个方框的作用
4个方框对应前面描述的Edit Layer面板中的几个参数。除了第4个颜色标识方框外，其他三个都可以通过单击来切换。

Visible
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-07.jpg">}}
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-08.jpg">}}
Hide On Playback
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-09.jpg">}}
Display Type
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-10.jpg">}}
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-11.jpg">}}
Color
{{< figure src="/img/20171114-[Maya]Channel Box & Layer Editor/[Maya]Channel Box & Layer Editor-12.jpg">}}

***
`无形者，形之君也。无端者，事之本也。---《战国策》`