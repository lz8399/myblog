+++
title= "[Maya]Snap操作"
date= "2017-08-31T15:15:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

##### 场景网格的显示与隐藏
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-01.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-02.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-03.jpg">}}

##### Snap To Grids（快捷键X按住不放）
点击Snap To Grids，表示物体移动时吸附场景的网格来移动，就是说移动的最小单位距离为一个方格大小。如果只是临时需要启用Snap To Grids，可以按住X键不放，等操作完了在松开X键。X键表示Snap to Grids取消或者选中：如果当前Snap 拖Grips未选中，按住X键就表示选中，否则相反。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-04.jpg">}}

如果要快速的拖动物体移到某个网格位置，可以按住X键不放，然后再在网格位置出按住鼠标中间并短距离的拖动以下。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-05.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-06.jpg">}}

##### Snap To Curves（快捷键C按住不放）
假设有个场景有个平面物体。我们在物体旁边画一条曲线。  
先点击：Create -》 Curve Tools -》 CV Curve Tool，
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-07.jpg">}}

然后鼠标左键依次点击多个点，形成一条曲线，
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-08.jpg">}}

生成好以后，再点击鼠标右键，弹出菜单中，选择Complete Tool。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-09.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-10.jpg">}}

然后再选中平面的一个顶点
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-11.jpg">}}

然后选中Snap to Curves（或者按住C键不放）：
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-12.jpg">}}

然后再把鼠标悬停在曲线上，并按住鼠标中键不放，来回滑动，就可以将选中的顶点沿曲线滑动。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-13.jpg">}}

在Snap to Curves模式下，除了可以吸附曲线滑动，也可以吸附其他的物体的边沿直线来滑动。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-14.jpg">}}

##### Snap to Points（快捷键：V键按住不放）
比如，相对两个平面的物体的边做缝合操作。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-15.jpg">}}

鼠标右键选择Vertex，切换到顶点模式。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-16.jpg">}}

再选择Move Tool，快捷键W。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-17.jpg">}}

再选中要缝合的点。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-18.jpg">}}

点击Snap to Points，或者按住V键不放。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-19.jpg">}}

然后把鼠标悬停在要另外一个物体要缝合的点上，比如红框标识的位置，然后再按住鼠标中键不放，小距离拖拽一下。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-20.jpg">}}

这样就可以把两个点连接在一起。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-21.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-22.jpg">}}

两条边上的点都连接好以后，切换到Object Mode，
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-23.jpg">}}

然后选中两个物体。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-24.jpg">}}

然后再按住shift键+鼠标右键，选择Target Weld Tool。即可完成缝合
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-25.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-26.jpg">}}
