+++
title= "[Maya]Polygon建模的常用操作与命令"
date= "2017-09-02T18:00:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++


Maya版本为2018

##### Bevel Edge倒角
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-01.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-02.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-03.jpg">}}

倒角的大小有参数Fraction控制，默认是0.5（边线的二分之一处），如果改成0.1（边线的十分之一处）则倒角会变小
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-04.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-05.jpg">}}

也可以把Offset as Fraction关掉，通过Offset来设置倒角的大小，效果一样。
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-06.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-07.jpg">}}

##### Insert Edge Loop插入环形边线
两种方式，一种是在Object Mode模式下，Shift + 鼠标右键 -》 Insert Edge Loop Tool，一种是点击菜单Mesh Tools-》 Insert Edge Loop。
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-08.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-09.jpg">}}

然后在按住鼠标左键在需要插入的位置上拖动。
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-10.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-11.jpg">}}

##### Edge Ring and Split 插入中线
先选中要插入中线的边
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-12.jpg">}}

再按住Ctrl键+鼠标右键，选择Edge Ring Utilities，
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-13.jpg">}}

再选择To Edge Ring and Split。
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-14.jpg">}}

效果
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-15.jpg">}}

##### Extrude Face挤压面
先选中面
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-16.jpg">}}

然后按住shift+鼠标右键，选择Extrude Face
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-17.jpg">}}

然后拖动坐标轴
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-18.jpg">}}

默认是挤压出的面是黏在一起的，如果想让选中的面分开挤压，再按住Ctrl+Shift+鼠标右键，选择`Toggle Keep Faces Together`。 
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-19.jpg">}}

效果：
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-20.jpg">}}

如果想合并，再执行一次`Toggle Keep Faces Together`。

##### To Edge Ring and Collapse 收边
先选中要收的边，然后按住Ctrl键 + 鼠标右键，选择Edge Ring Utilities -》 To Edge Ring and Collapse。
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-21.jpg">}}
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-22.jpg">}}

然后选中的边和旁边的两条边会合并并等分分成两条边
{{< figure src="/img/20170902-[Maya]Polygon建模的常用操作与命令/[Maya]Polygon建模的常用操作与命令-23.jpg">}}
