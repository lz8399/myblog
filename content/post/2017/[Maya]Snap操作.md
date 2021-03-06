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

##### Snap To Grids 技巧1
比如你想用Multi-Cut沿着网格投射出一条线，但是你希望的投射线段的起点对应的Grid网格正好再模型内部且周围点和线较多（途中黄圈部位），这是你把鼠标悬停在这个网格位置处，maya不一定会自动帮你吸附到这个网格，这个时候的解决办法为：
从模型外的网格投射，然后再删掉不想要的部分。比如把图中两个红圈所示的位置当作起点进行投射，这样maya就会自动帮你吸附在这两个位置处。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-06-02.jpg">}}

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

然后执行Combine（Mesh -》 Combine）
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-25.jpg">}}

然后框选要缝合的点。  
{{< alert danger >}}注意：一定要框选，如果一个个单击则选择的是单个点，而不是两个重合的点。{{< /alert >}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-26.jpg">}}

然后执行Merge，则可以将两个点合并
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-27.jpg">}}

为了验证是否真的合并，可以点击选择一个点上下拖动，看是否合并成功
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-28.jpg">}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-29.jpg">}}

如果不成功，则效果是这样的：
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-30.jpg">}}

##### Snap to Points 案例2
假设有这样一个模型
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-31.jpg">}}

我们希望下面两条左右两条边变为垂直而不是倾斜，比如这样
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-32.jpg">}}

做法：
1，先选中边
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-33.jpg">}}
2，再选中要移动的轴向
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-34.jpg">}}
3，按住V键不放，并且按住鼠标中间（滚轮），沿选中轴向的方向回来拖动。
{{< alert warning >}}如果目标移动的不明显，则来回拖动的幅度可能要大一点，幅度小了可能吸附的幅度也较小，看不出效果。如果目标移动的幅度太大，则拖动鼠标的时候慢一点，否则可能会错误最佳位置。{{< /alert >}}
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-35.jpg">}}
拖动过程中，边会自动吸附相应的位置，直到吸附在的我们想要的垂直效果的位置，即算完成。
{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-36.jpg">}}

{{< alert success >}}还有另外一种方式来代替上面的第2步和第3步，方式如下：
按住V键不放，然后鼠标左键单击要移动的轴向箭头并按住不放，然后再沿轴向方向来回拖动。{{< /alert >}}

{{< alert warning >}}注意：上述案例中，当旋转的半径较长时，在拖动过程中Snap吸附可能不是很灵敏，这种情况下，需要将光标拖拽（按住坐标轴后再拖拽）到我们期望对齐的位置（下图中红圈所示范围内）。如果拖拽到该位置后还未达到预期，再左右拖拽调整下。{{< /alert >}}

{{< figure src="/img/20170831-[Maya]Snap操作/[Maya]Snap操作-37.jpg">}}

***
`玉骨西风，恨最恨、闲却新凉时节。---周密《玉京秋》`