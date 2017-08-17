---
title: "[ZBrush]ZModeler Bridge-桥接处理"
date: "2017-08-15T17:28:42+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
--- 

Keyword：zbrush、zmodeler

##### Bridge（桥接）
**两个边连接**

假设有这样一个平面：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-01.jpg">}}

先把鼠标悬停在点上，然后按住空格键不放，选择如下：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-02.jpg">}}

然后鼠标在Point上按住不放拖拽，就可以拉出一个圆：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-03.jpg">}}

然后在另外一个Point单击以下，即可自动生成上次画的圆：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-04.jpg">}}

然后鼠标悬停在Polygon上，按住空格键不放，选择如下：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-05.jpg">}}

然后挨个挨个单击需要删除Polygon：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-06.jpg">}}

然后鼠标悬停在Edge上，按住空格键不放，选择如下：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-07.jpg">}}

然后鼠标在需要桥接的两个Edge上分别单击一下：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-08.jpg">}}
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-09.jpg">}}

单击后就会自动生成一个新的Polygon：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-10.jpg">}}

用同样的方式，再对另一边形成以上操作，就可以创建出一个类似机械插槽的效果：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-11.jpg">}}

<font color=red>注意：再Bridge之前，确保当前模型是一个独立的instance，如果有隐藏的部位与当前模型相连，请先确保执行过Del Hidden，否则无法Bridge成功。</font>


**两个洞连接**

假设存在这样的模型：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-12.jpg">}}

然后鼠标悬停在Edge上，按住空格键不放，选择如下：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-13.jpg">}}

然后分别单击以下左右两个洞的边：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-14.jpg">}}
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-15.jpg">}}


当单击第二个洞的边时，同时鼠标按住不放，就会生成如下效果：
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-16.jpg">}}

此时再拖拽鼠标：<font color=red>上下拖改变密度，左右拖改边高度。</font>
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-17.jpg">}}
{{< figure src="/img/20170815-[ZBrush]ZModeler Bridge-桥接处理/[ZBrush]ZModeler常用操作示例-02-18.jpg">}}
