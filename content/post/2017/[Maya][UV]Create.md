+++
title= "[Maya][UV]Create"
date= "2017-10-31T16:29:40+08:00"
categories= ["Maya"]
tags= ["Modeling", "UV"]
keywords= ["Maya", "分UV", "展UV", "创建UV"]
+++

Maya版本为2018.1

假设找分UV的模型如下
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-01.jpg">}}
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-02.jpg">}}

在UV Toolkit面板中展开Create选项
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-03.jpg">}}

{{< alert warning >}} 注意，每次之前Create之前，需要框选中需要分UV的面或者Object。如果是整个物体，则框选所有面或者选中Object，然后执行Create命令。只框选顶点不起作用。 {{< /alert >}}

不同的Create方式效果如下：

+ Automatic
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-04.jpg">}}

+ Cylinderical
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-05.jpg">}}

+ Spherical
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-06.jpg">}}

+ Camera-Based
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-07.jpg">}}

+ Normal-Based
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-08.jpg">}}

+ Planar
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-09.jpg">}}

+ Best-Plane  
先框选需要处理的对象
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-10.jpg">}}
然后点击Best-Plane，此时会提示你选择一个面或者三个顶点作为投射方向，来确定投射的方向
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-11.jpg">}}
选择好面或者3个顶点之后，再按回车，则maya会自动按照这个投射方向来创建UV。
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-12.jpg">}}

+ Contour Stretch  
先选中需要切割的区域
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-13.jpg">}}
然后执行Contour Stretch
{{< figure src="/img/20171031-[Maya][UV]Create/[Maya][UV]Create-14.jpg">}}

