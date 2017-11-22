+++
title= "[Maya]Harden Edge和Softend Edge区别"
date= "2017-09-08T19:04:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya", "硬边", "软边", "3DMax smoothing group", "光滑组"]
+++

keywords：Maya、硬边、软边、3DMax smoothing group、光滑组


简单的说就是：多个面是否公用法线，硬边不共用法线，软件共用法线。Maya的软硬边相当于Max和Blender中的光滑组（Smoothing Groups）。

以下面的球体为例
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-00-01.jpg">}}

如果是硬边，则顶点在不同的面的方向上，都有对应的独立的法线。（显示顶点法线：Display -》 Polygons -》 Vertex Normals）
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-00-02.jpg">}}
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-00-03.jpg">}}

如果是软边，一个顶点关联的不同的面，即使面的方向不同，这个顶点也只有一根法线。
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-00-04.jpg">}}

{{< alert success >}}
软边的好处是：烘焙法线时，如果硬边位置的UV没有断开，则法线有明显接缝，如果硬边位置的UV不想断开，且又不希望烘焙法线时有明显接缝，那么就可以是将该位置改为软边。
{{< /alert >}}

##### 官方解释

{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-01.jpg">}}

官方文档：  
Edit the vertex normals to affect polygon shading  
http://download.autodesk.com/global/docs/maya2014/en_us/index.html?url=files/Editing_polygons_Edit_the_vertex_normals_to_affect_polygon_shading.htm,topicNumber=d30e163432

##### 执行Harden Edge/Soften Edge的方式
选中边以后，Display -》 Polygons -》 Soft/Hard Edges
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-02.jpg">}}

或者在选中边之后按住Shitf+鼠标右键 -》 Soften/Harden Edges
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-03.jpg">}}
{{< figure src="/img/20170908-[Maya]Harden Edge和Softend Edge区别/[Maya]Harden Edge和Softend Edge区别-04.jpg">}}
