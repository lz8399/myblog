+++
title= "[Maya]Select"
date= "2017-09-09T20:30:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

##### Selection Constraints
+ Border  
假如有如下物体，一个面删掉了，现在我们想选中这个面的边界，也就是4条边。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-01.jpg">}}

然后Ctrl+Shift+鼠标右键，选择：Selection Constraints -》 Border
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-02.jpg">}}

这样将鼠标放在边界上，就可以自动地同时选中4条边。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-03.jpg">}}

+ Edge Loop（快捷键：鼠标左键双击）  
表示选中封闭的环形边线
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-04.jpg">}}

+ Edge Ring  
表示选中环形表面的独立边线
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-05.jpg">}}

##### 批量选择
鼠标左键双击一个面，表示选中整个物体。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-06.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-07.jpg">}}

选中一个面之后再按住shift键，鼠标左键双击相邻的另外一个面，表示选中这一圈的所有面。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-08.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-09.jpg">}}

选择一个面，然后按住shift键，鼠标左键双击另外一个不相邻的面，则表示选中两个面之间的所有面。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-10.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-11.jpg">}}

选择共点面
比如圆柱体的上下两个面
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-12.jpg">}}

批量选择共点面方式有多种：

+ 方式1：直接框选  
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-13.jpg">}}
    缺点是投射的方向也会被框选
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-14.jpg">}}

+ 方式2：To Faces  
    先切换至Vertex，然后选中中心点，按住Ctrl+鼠标右键，选择To Faces -》 To Faces。
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-15.jpg">}}
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-16.jpg">}}
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-17.jpg">}}


    同样的方式也可以用来选中共点线，即To Edges。  
    还可以选择共点点，即To Vertices。  

+ 方式3：Ctrl + F11  
    选中中心点，然后按Ctrl + F11
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-18.jpg">}}
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-19.jpg">}}

    同样的方式，Ctrl + F10是选中所有的共点边
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-20.jpg">}}

    Ctrl + F9是从选中的面或线中选取关联的所有点。  
    比如这里选中了了圆柱顶部的所有面，现在想选中这些面相关的所有点，则可以按Ctrl+F9
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-21.jpg">}}
    {{< figure src="/img/20170909-[Maya]Select/[Maya]Select-22.jpg">}}

##### Lasso 套索
先按Q键，切换到Select Tool模式，然后按住Ctrl+Shift+鼠标右键，选择Lasso
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-23.jpg">}}

然后就可以用套索选择点、线、面了。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-24.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-25.jpg">}}

##### 加选、减选、强制加选
以Face面选择为例，此方式同样适用与点和边的选择

+ 加选：Shift+鼠标左键框选。如果框选的区域之前未选中，则框选后变为选中
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-26.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-27.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-28.jpg">}}

+ 减选：Ctrl+鼠标左键框选。如果框选的区域之前已经选中，则框选后变为未选中
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-29.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-30.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-31.jpg">}}

+ 强制加选：Ctrl+Shift+鼠标左键框选。不管框选的点线面有没被选中，统一变为选中
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-32.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-33.jpg">}}
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-34.jpg">}}

##### 全选和取消全选
快捷键Ctrl + Shift + A，表示选中场景内所有的模型。
Alt + D，取消所有选择。
{{< figure src="/img/20170909-[Maya]Select/[Maya]Select-35.jpg">}}



