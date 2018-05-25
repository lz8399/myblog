+++
title= "[Maya]Edit"
date= "2017-08-29T18:20:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++
 
 
##### Repeat 上一次执行的操作（G键）
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-01.jpg">}}

比如我们对某条边执行了Bevel操作，
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-02.jpg">}}

相对另一条边也执行同样的操作，可以选择该边后，按G键，就会自动重复上次的操作。
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-03.jpg">}}

##### Duplicate复制（Ctrl + D）
复制一个物体，快捷键Ctrl + D，相当于Ctrl + C再Ctrl + V的效果。
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-04.jpg">}}

##### Duplicate with Transform 变换复制（Shift + D）
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-05.jpg">}}

比如我们先按下Ctrl + D，复制出一个模型出来，然后再拖动一段距离：
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-06.jpg">}}

然后再按shift + D，那么就会自动复制一个模型且复制上一次执行的Transform操作
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-07.jpg">}}

{{< alert danger >}}注意，Duplicate With Transform不止对Move操作有效，对Rotate、Scale操作也有效。{{< /alert >}}
{{< alert info >}}G键虽然也是重复上一次操作，但是它只会复制，不会进行执行移动。{{< /alert >}}

##### Duplicated Special 特殊复制（Ctrl + Shift + D）
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-08.jpg">}}

打开其参数面板后，可以设置复制时旋转的角度和个数等信息，然后一次性生成。相当于Shift+D的批量执行。
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-09.jpg">}}

##### Duplicated Special之Instance
假设我们有这个细分级别为20的圆柱
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-10.jpg">}}

现在只保留一个细分段，其他都删掉
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-11.jpg">}}

然后设置参数：

+ Geometry type修改为Instance；
+ 修改旋转角度，因为我们细分级别是20,360度除以20等于18；
+ 复制一圈需要20个，所以还需要再复制19个。
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-12.jpg">}}

这样复制出来的的每个小块，就可以同时编辑了
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-13.jpg">}}

比如选中任意某个顶点，就会自动选中一圈的所有顶点
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-14.jpg">}}

移动一个顶点，其他顶点也会做轴对称移动
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-15.jpg">}}

操作面或线时也会有轴对称变化的效果
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-16.jpg">}}

{{< alert warning >}}注意：复制出来的对象都是一个个独立的Object，如果要最终合并下，需要执行Combine。{{< /alert >}}

***
`怀重宝者不以夜行，任大功者不以轻敌。---《战国策》`