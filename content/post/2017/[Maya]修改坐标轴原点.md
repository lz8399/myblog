+++
title= "[Maya]修改坐标轴原点"
date= "2017-08-29T20:21:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

##### 方式一：Insert
默认坐标轴中间在模型底部的正中间位置，
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-01.jpg">}}

如果想改变坐标轴原点位置，先把物体挪开，然后再按下insert键
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-02.jpg">}}

此时就可以移动坐标轴
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-03.jpg">}}

确定好新的坐标世界坐标原点后，再按一次insert键，即可完成修改。
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-04.jpg">}}

技巧：如果移动过程中，希望坐标轴能一个网格一个网格的移动，而不是随意距离拖动，点击Snap to Grids（快捷键：按住X键不放）。
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-05.jpg">}}

##### 方式二：Reset Transformation
先将物体移动后，先执行：Modify -》 Freeze Transformations，再执行：Modify -》 Reset Transformations。
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-06.jpg">}}

执行后坐标轴原点就会自动变为初始时的位置。
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-07.jpg">}}

##### 方式三：快捷键D
与Insert键一样，但是相对Insert键按起来更方便，因为Insert键离字母键区域较远。

##### 坐标轴相对物体居中
{{< figure src="/img/20170829-[Maya]修改坐标轴心点/[Maya]修改坐标轴心点-08.jpg">}}
