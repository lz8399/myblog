+++
title= "[Maya]小技巧合集(个人零散笔记)"
date= "2017-11-12T15:56:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya"]
+++

Maya版本为2018

##### To Faces 选中圆柱顶部的所有面
先选中顶部中心的顶点
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-01.jpg">}}
然后按住Ctrl+右键连续向下拖拽两次
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-02.jpg">}}
就可以选中顶部的所有面
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-03.jpg">}}

##### Collapse Edge 塌陷处理
假如有个这样的结构
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-04.jpg">}}
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-05.jpg">}}

我们希望处理的效果如下：
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-06.jpg">}}
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-07.jpg">}}

处理方式如下：  
先选中要塌陷处理的边。因为这里假设是对称结构，所以我选择了两条边，如果你只需要对某一边做塌陷，那么只选择一条边即可。
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-08.jpg">}}

然后按住Shift+鼠标右键：
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-09.jpg">}}
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-10.jpg">}}

如上所述：如果是单条边线塌陷，则这条线的两端的顶点在边线中点位置合并为一个点。
如果是选择多条连续的边，则这些边会全部消失并缩成一个顶点。例如：
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-11.jpg">}}
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-12.jpg">}}
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-13.jpg">}}

##### 圆角矩形的高模低模布线
高模
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-14.jpg">}}
低模
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-15.jpg">}}

##### 环形凹凸平面压平
比如有如下结构，现在需要拓扑低模，圆柱顶部的凹凸结构改成一个简单的圆形平面。
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-16.jpg">}}
做法如下：
先删掉顶部的除边界外的所有环线
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-17.jpg">}}
然后再删除顶点
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-18.jpg">}}
然后再切换到侧视图中将圆形的中心点移动与边沿齐平的位置。
{{< figure src="/img/20171112-[Maya]小技巧合集(个人零散笔记)/[Maya]小技巧合集(个人零散笔记)-19.jpg">}}

***
`惟有楼前流水，应念我、终日凝眸。凝眸处，从今又添，一段新愁。---李清照《凤凰台上忆吹箫》`