+++
title= "[UE4]物体跟随Spline路径移动(Move Along Spline Path)"
date= "2018-03-04T13:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Spline"]
+++

先建一个普通的Actor蓝图，然后再蓝图中添加Spline Component（注意：不是Spline Mesh Component）
{{< figure src="/img/20180304-[UE4]物体跟随Spline路径移动(Move Along Spline Path)/[UE4]物体跟随Spline路径移动(Move Along Spline Path)-01.jpg">}}

然后编辑路径，如果要添加新节点，右键路径 -》 Add Spline Point Here。
{{< figure src="/img/20180304-[UE4]物体跟随Spline路径移动(Move Along Spline Path)/[UE4]物体跟随Spline路径移动(Move Along Spline Path)-02.jpg">}}

然后把该Actor蓝图拖到场景中，然后在相应蓝图（比如角色蓝图）中编辑移动逻辑：
{{< figure src="/img/20180304-[UE4]物体跟随Spline路径移动(Move Along Spline Path)/[UE4]物体跟随Spline路径移动(Move Along Spline Path)-03.jpg">}}
(图片放大：复制图片地址单独打开)

##### 将Spline 曲线打直（Turn Splines curves into straight Spline paths）

选中需要打直的曲线，在Detail面板中找到：Selected Points -》 Type，修改为Linear，默认为Curve。

***
`君子和而不同，小人同而不和。 ----《论语》`