+++
title= "[Maya]Edit Mesh"
date= "2017-09-08T16:56:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-01.jpg">}}

##### Extrude 挤压
表示在原有物体上挤压出新的形状。
先选中需要挤压的面
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-02.jpg">}}

然后点击 Edit Mesh -》 Extrude（Ctrl + E），或者Shift + 鼠标右键 -》 Extrude Face
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-03.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-04.jpg">}}

然后拖动坐标轴
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-05.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-06.jpg">}}

其中，右上角的小圆圈表示坐标轴类型，默认是当前面朝向的坐标轴，点击一下可切换到世界坐标轴
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-07.jpg">}}

挤压后可以设置的3个常用属性：Offset、Divisions、Thickness
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-08.jpg">}}
Offset=0.3
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-09.jpg">}}
Divisions=11
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-10.jpg">}}
Thickness=3
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-11.jpg">}}

除了可以直接修改数值，还可以用鼠标拖动：
先选中属性名
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-12.jpg">}}
然后鼠标悬停在输入栏，光标会变成表示可左右拖动的样式，然后按住鼠标左键左右拖动
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13.jpg">}}

##### Extrude挤压和Scale伸缩结合使用
假设我们想用圆柱体挤压出这样的效果
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-02.jpg">}}

方式如下：  
先选中面，然后Ctrl+E挤压
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-03.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-04.jpg">}}

此时不用拖动坐标轴，而是按下R键切换到Scale模式
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-05.jpg">}}

然后按住中间的黄色小方块拖拽
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-06.jpg">}}

然后再按Ctrl+E，然后再拖动向上的坐标轴
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-07.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-13-08.jpg">}}

##### Extract提取
表示将面从物体中分离并提取出来。
先选中面
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-14.jpg">}}
然后点击Edit Mesh -》 Extract
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-15.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-16.jpg">}}

此时再拖动坐标轴，就可以将选中的面提取出来
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-17.jpg">}}

##### Average Vertices
当顶点分布不均匀时，通过Average Vertices可以是顶点重新分布均匀
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-18.jpg">}}

选中需要均匀分布的顶点，然后点击：Edit Mesh -》 Average Vertices。
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-19.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-20.jpg">}}

多次点击可以可使顶点逐步均匀，直至和周围的布线统一。
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-21.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-21-2.jpg">}}

##### Bridge桥接
假设有两个正方体，对立的两个面都是开口的。
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-22.jpg">}}
先将两个模型Combine（Mesh -》 Combine）
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-23.jpg">}}
然后选中两个模型的开口的4条边
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-24.jpg">}}
然后在点击：Edit Mesh -》 Bridge
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-25.jpg">}}

##### Project Curve on Mesh
演示示例
先新建一个球体，和一个圆形曲线
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-26.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-27.jpg">}}

调整曲线的位置和旋转
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-28.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-29.jpg">}}

然后切换到需要投射方向的视图
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-30.jpg">}}

然后同时选中球体和圆圈
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-31.jpg">}}

然后再点击Edit Mesh -》 Project Curve on Mesh
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-32.jpg">}}

这样在球体上就投射形成了一个特殊曲线
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-33.jpg">}}

然后再选中球体和球体上的曲线，选中方式：按住鼠标左键框选曲线和球体，不要点击球体
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-34.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-35.jpg">}}

如果单击球体，选中状态就是这样的（这种情况下无法进行后续的操作）：
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-36.jpg">}}

然后点击Edit Mesh -》 Split mesh with projected curve
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-37.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-38.jpg">}}

然后拖动球体，是原本的曲线与球体分离开
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-39.jpg">}}

然后再切换到侧向视图，
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-40.jpg">}}

选中要删除的面，并删除
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-41.jpg">}}
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-42.jpg">}}

这样就挖出了一个特殊形状的开口
{{< figure src="/img/20170908-[Maya]Edit Mesh/[Maya]Edit Mesh-43.jpg">}}
