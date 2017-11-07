+++
title= "[Maya][UV]Select"
date= "2017-11-05T17:27:40+08:00"
categories= ["Maya"]
tags= ["Modeling", "UV"]
keywords= ["Maya", "分UV", "展UV", "选择", "Selection"]
+++

Maya版本为2018.1

在UV Toolkit的顶部，是UV选择模式的按钮
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-01.jpg">}}

##### Selection 选择模式
左边三个是建模时的点、线、面选择模式
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-02.jpg">}}
右边两个分别是UV编辑模式下的点选择、UV壳选择。
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-03.jpg">}}

在建模模式下，选择点、线的时候，maya会自动帮你选中其他UV壳上与之公用的点、线。
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-04.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-05.jpg">}}

如果UV模式下，选择点，则不会选中其他UV壳上与之关联的点。
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-06.jpg">}}

{{< alert info >}} 
建模模式下选中的点为黄色，UV模式下选中的点为绿色。
{{< /alert >}}

##### All/Clear/Inverse 全选、清除、反选
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-07.jpg">}}

+ All 全选（Ctrl + Shift + A）
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-08.jpg">}}
+ Clear 清除
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-09.jpg">}}
+ Inverse 反选
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-10.jpg">}}
{{< alert info >}} 
注意：多边形建模时的Ctrl、Shift、Ctrl+Shift框选方式同样对UV适用。例如按住Shift反选。
{{< /alert >}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-11.jpg">}}


##### Shrink/Grow Selection 收缩/扩张选择模式
在UV Toolkit面板中有以下几种
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-12.jpg">}}

+ Grow Selection along loop （第4个）
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-13.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-14.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-15.jpg">}}
+ Grow Selection （第3个）
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-16.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-17.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-18.jpg">}}
+ Shrink Selection （第2个）
相当于Grow Selection的倒序操作。  
如果是这种情况下执行Shrink Selection，则会全部一次性全部取消选中。  
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-19.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-20.jpg">}}
+ Shrink Selection along loop（第1个）  
相当于Grow Selection along loop的倒序操作。

##### Symmetry 对称
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-21.jpg">}}
其中Topology意思是拓扑对称，用法如下：  
先选择一条线作为对称轴
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-22.jpg">}}

选中后，然后点击：Symmetry -》 Topology，此时Symmetry会变成当前物体的对象名。
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-23.jpg">}}

然后就可以以这条线为对称轴选择目标了
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-24.jpg">}}

##### Selection Constraint 选择约束
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-25.jpg">}}
可以更详细的指定选择对象的限定类型，比如：正面、反面、几何边框、贴图表框等等。

+ Back-Facing 法线反转的面
假设物体上有的面的法线方向反转了
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-26.jpg">}}
那么在Back-Facing约束下，框选时只能选择这些反转的面。
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-27.jpg">}}
+ Front-Facing 法线方向正常的面
+ Geometry Borders 不清楚，待查资料
+ Texture Borders 贴图表框。也就是UV壳边框。  
如果是在面选择模式下，那么就是选中的UV壳一圈的面
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-28.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-29.jpg">}}
如果是在线选择模式下，那么就是选中的UV壳一圈的边框
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-30.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-31.jpg">}}
+ UV Edge Loop UV的横向环线
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-32.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-33.jpg">}}
+ UV Edge Ring UV的纵向环线
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-34.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-35.jpg">}}
+ UV Shell UV壳
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-36.jpg">}}

##### Transform Constraint 变化约束
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-37.jpg">}}
如果Transform Constraint关闭，那么选择的区域可以任意拖拽
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-38.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-39.jpg">}}

如果开启约束，则边框被固定住无法变换，边框之外的区域可以正常变换。  
向下拖动
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-40.jpg">}}
向上拖动
{{< figure src="/img/20171105-[Maya][UV]Select/[Maya][UV]Select-41.jpg">}}
