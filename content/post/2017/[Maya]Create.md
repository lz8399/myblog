+++
title= "[Maya]Create"
date= "2017-10-06T20:14:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++


Maya版本为2018
##### Create Polygon Primitives
Create -》 Polygon Primitives可以直接创建常规物体。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-01.jpg">}}

如果勾选Interactive Creation，则表示创建时可以通过鼠标手势来指定物体的初始大小，但是需要两步：先按住鼠标左键拖拽来设置底部的大小，然后松开鼠标再按住不放拖拽，来设置高度。也可以单击一下鼠标左键直接生成默认大小的模型。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-02.jpg">}}
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-03.jpg">}}

Create Polygon的hotbox操作是：按住shift+鼠标右键，这里也可以勾选Interactive Creation。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-04.jpg">}}

##### Create Image Plane
Image Plane是一个可以放置图片的平面，可以将三视图放置在里面，以便在建模过程中有物体的大小、比例、位置等参考信息。  
Create -》 Free Image Plane创建一个Image Plane。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-05.jpg">}}
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-06.jpg">}}

然后打开Image Plane的Attribute面板
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-07.jpg">}}
然后设置图片路径
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-08.jpg">}}
效果
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-09.jpg">}}
我们把图片位置调整后，不希望其位置、大小可编辑，而是将其锁定，可以Channel Box中选择相应属性，然后选择Lock Selected。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-10.jpg">}}

**另外一种锁定方式：**  
打开Channel Box，在display标签页中选择Create a new layer。这个Layer类似PS的图层。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-11.jpg">}}
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-12.jpg">}}

然后选中Image Plane
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-13.jpg">}}

然后再右键layer，选择Add Selected Objects
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-14.jpg">}}

然后将第3个方框切换为R（通过单击来切换），R表示不可选中。这样也可以防止Image Plane被编辑。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-15.jpg">}}

T表示隐藏
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-16.jpg">}}
空白表示可选中
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-17.jpg">}}
另外，最左边的V按钮表示隐藏或显示Layer。

另外，一般情况下不希望Image Plane在透视图中显示，而是只在前视图中显示，那么可以在Attribute面板中设置Display，选中Looking through camera并设置值为front，这样可以让图片只在front视图中显示。
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-18.jpg">}}
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-19.jpg">}}
{{< figure src="/img/20171006-[Maya]Create/[Maya]Create-20.jpg">}}

