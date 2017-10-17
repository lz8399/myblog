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

打开其参数面板后，可以设置复制时旋转的角度和个数，然后一次性生成。相当于Shift+D的批量执行。
{{< figure src="/img/20170829-[Maya]Edit/[Maya]Edit-09.jpg">}}