---
title: "[ZBrush]ArrayMesh和WeldPoint"
date: "2017-08-16T10:40:42+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
--- 

Keyword：zbrush、ArrahMesh、WeldPoint、阵列、顶点缝合、接缝

假设有这样一个扇形，我们希望以扇形圆心为中心，旋转360度复制出N个，形成一个完整的圆：
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-01.jpg">}}

步骤如下：  
1，先点击Tool -》 ArrayMesh -》同时启用 Array Mesh 和Transpose：
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-02.jpg">}}

2，在点击Pivot，模型中间就会出现一个黄色的圆圈，表示的是当前模型的坐标轴原点：
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-03.jpg">}}
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-04.jpg">}}

3，这个原点默认在模型的正中间。但是我们希望原点在扇形下边顶角处，则我们可以修改X、Y或Z的值。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-05.jpg">}}

这里将Y修改为-0.5，表示将原点向下移动整个模型长度的一半，如果是0.5，则表示向上移动一半。如果不确定到底是X还是Y或者Z，随便改下数值试一下就明白了。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-06.jpg">}}

4，然后点击Rotat，表示旋转，然后把需要选择方向的轴向修改为360度。这里示例中是Z轴，如果不清楚，3个轴改下数值试一下就清楚了。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-07.jpg">}}

5，修改为360度后的默认效果。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-08.jpg">}}

6，此时只有两个模型的实例。这是因为Repeat的默认数值为2，我们希望复制多个，那么就修改Repeat的值，比如值为8时，效果如下：
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-09.jpg">}}
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-10.jpg">}}

7，Repeat为16时，效果如下：
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-11.jpg">}}
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-12.jpg">}}

8，此时并得到了预期的效果，此时再点击Make Mesh，表示将之前的复制出来的镜像转换为模型对象。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-13.jpg">}}
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-14.jpg">}}

9，到此还没完，我们发现当执行Dynamic时（快捷键D，Shift+D表示去掉Dynamic），每个扇形之间是有缝隙的。原因是我们Make Mesh之后没有做接缝处理。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-15.jpg">}}

10，我们再修改WeldDist数值，表示顶点缝合的最大距离，在这个距离之内的两个点合并成一个点。然后再点击WeldPoints，执行顶点风格。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-16.jpg">}}
此时再执行Dynamic，可以看到每个扇形的边沿没有裂开了，已经合并成了一个整体。
{{< figure src="/img/20170816-[ZBrush]ArrayMesh和WeldPoint/[ZBrush]ArrayMesh和WeldPoint-17.jpg">}}
