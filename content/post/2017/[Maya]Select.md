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