+++
title= "[Maya]补洞后的补线技巧"
date= "2017-10-17T19:58:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya Fill Hole", "Edge Loop", "Append To Polygon"]
+++

Maya版本为2018

假如一个物体删面后的结构如下，现在需要对其进行补洞
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-01.jpg">}}

如果用Append to Polygon或者Fill hole，其效果如下。中间的两条环线断开了，需要自己补上断开的环线
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-02.jpg">}}

##### 等分环线的补线
如果环线的位置是在等分的位置，比如当前例子中假设两条环线是在物体宽度的三分之一处，那么可以线上添加等分的顶点：选中线后，按住Shift+鼠标右键 -》 Add Divisions To Edge
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-03.jpg">}}

然后设置需要的顶点数量，执行Add Divisions。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-04.jpg">}}

这样就可以在线上生成两个顶点，然后就可以用Multi-Cut连线了。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-05.jpg">}}

##### 非等分环线的补线
但是假如环线的位置不是等分的，那么用Add Divisions的方式就无法使用。  
解决办法如下：
先选中洞的一条边，然后挤压（Ctrl+E）
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-06.jpg">}}

然后向洞的另一边的方向拖动，等拖到第一条环线位置处附近时，使用Snap To Point（V键）进行吸附，使挤压出来的线正好和环线的位置重合。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-07.jpg">}}

然后再挤压一次，重复上述的操作，直到整个洞全部补齐。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-08.jpg">}}
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-09.jpg">}}
{{< alert danger >}}挤压完毕后记得合并顶点：选择所有顶点，然后按住Shift+鼠标右键 -》 Merge Vertices -》 Merge Vertices。{{< /alert >}}

在挤压过线的过程中，可能会产生法线方向朝内的面，这些面为黑色，把这些黑色的面反转一下（{{< hl-text green>}}Mesh Display -》 Reverse{{< /hl-text >}}）。  
如果有的面是黑白相间的阴影，则说明这里有两个重合的面且两个面的法线方向时相反的，需要先删掉一个面，然后如果仍然时黑色则再反转一次，直到所有的面都变为正常光影的面。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-10.jpg">}}
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-11.jpg">}}

面反转完后，然后按3看下平滑效果，看每个面是否有异常，如果有异常，且之前已经合并过顶点，则说明面有问题：两个重合的面且法线方向是正常的。
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-12.jpg">}}

那么就需要删掉异常位置处多余的面，然后再按3平滑一次按效果。正常效果如下：
{{< figure src="/img/20171017-[Maya]补洞后补线的技巧/[Maya]补洞后补线的技巧-13.jpg">}}