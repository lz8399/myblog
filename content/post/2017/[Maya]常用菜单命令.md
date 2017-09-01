+++
title= "[Maya]常用菜单命令"
date= "2017-08-29T18:20:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++
 
 
##### Repeat 上一次执行的操作
快捷键G
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-01.jpg">}}

比如我们对某条边执行了Bevel操作，
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-02.jpg">}}

相对另一条边也执行同样的操作，可以选择该边后，按G键，就会自动重复上次的操作。
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-03.jpg">}}

##### Duplicate复制
复制一个物体，快捷键Ctrl + D，相当于Ctrl + C再Ctrl + V的效果。
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-04.jpg">}}

##### Duplicate with Transform 变换复制
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-05.jpg">}}

比如我们先按下Shift + D，复制出一个模型出来，然后再拖动一段距离：
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-06.jpg">}}

然后再按shift + D，那么就会自动复制一个模型且复制上一次执行的Transform操作
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-07.jpg">}}

<font color=red>注意，Duplicate With Transform不止对Move操作有效，对Rotate、Scale操作也有效。</font>

##### 全选和取消全选
快捷键Ctrl + Shift + A，表示选中场景内所有的模型。
Alt + D，取消所有选择。
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-08.jpg">}}

##### Freeze Transformations
当物体执行Transform操作之后，Channel Box面板中的参数就会发生变化。例如：
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-09.jpg">}}
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-10.jpg">}}

如果此时就想以物体当前Transform为坐标轴的原点位置，Rotation也相当于初始时的Rotation，Scale也被当作为1，可以点击：Modify -》 Freeze Transformations。
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-11.jpg">}}

执行后，相关参数就会变化初始化的参数，但是物体的Transform不会变化。
{{< figure src="/img/20170829-[Maya]常用菜单命令/[Maya]常用菜单命令-12.jpg">}}
