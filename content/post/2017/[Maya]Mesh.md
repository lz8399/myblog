+++
title= "[Maya]Mesh"
date= "2017-10-02T12:01:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

##### Combine
假设有两个独立的物体，想把他们合并为一个整体。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-01.jpg">}}

先选中两个物体
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-02.jpg">}}

然后按住Shift + 鼠标右键，点击Combine
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-03.jpg">}}

这样两个物体就合并和一个整体，共享移动、伸缩、旋转等操作。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-04.jpg">}}

如果要分离两个物体，选中后按住Shift + 鼠标右键，点击Separate。

Combine和Separate的菜单位置再Mesh目录下：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-05.jpg">}}

##### Booleans
假设有两个物体相交在一起
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-06.jpg">}}

然后点击Mesh -》 Booleans，有三个选项：Union结合、Difference相减，Intersection相交。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-07.jpg">}}

+ Union 结合
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-08.jpg">}}

+ Difference 相减  
先选中的哪个物体，则保留哪个物体
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-09.jpg">}}

+ Intersection相交
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-10.jpg">}}


##### Triangulate和Quadrangulate（三角化/四角化）
假设有这样一个方框形状的模型，那么的某些面不是三角边也不是四角边
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-11.jpg">}}

如果需要将所有面转换为三角边或者四角边，点击：Mesh -》 Triangulate或者Quadrangulate
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-12.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-13.jpg">}}

##### Smooth （相当于ZBrush的Divide细分）
点击菜单Mesh -》Smooth，多次点击可多次平滑
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-14.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-15.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-16.jpg">}}

平滑的另外一种方式：  
先按3预览平滑效果
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-17.jpg">}}

然后点击：Modify -》 Convert -》 Smooth mesh preview to polygons
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-18.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-19.jpg">}}

##### Mirror
假如有个模型，需要沿Y轴方向做对称处理
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-21.jpg">}}

点击Mesh -》 Mirror，选中Y轴，点击apply
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-22.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-23.jpg">}}
{{< alert info >}}
Cut Geometry表示是否先剪切再复制，比如有个圆柱，顶部是凸的，底部是凹的，那么如果勾选Cut Geometry，那么沿圆柱纵向方向镜像时，顶部和底部会同时变为凹的或者凸的，如果不勾选，那么顶部和底部会同时保留凹和凸的结构。
{{< /alert >}}

其中，镜像时控制顶点缝合的属性是Merge Threshold。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24.jpg">}}

##### Mirror的相关参数
假设有这样一个物体，现在需要做镜像处理
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-02.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-03.jpg">}}

期望的效果如下：以世界坐标轴原点为基准，在X轴方向做对称
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-04.jpg">}}

则需要修改的参数为：

+ Mirror Axis Position修改为World
+ Combine With Original取消勾选
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-05.jpg">}}

如果期望效果如下：以物体自身坐标轴原点为基准，在X轴方向上做对称。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-06.jpg">}}

则需要修改的参数为：

+ Mirror Axis Position修改为Object
+ Combine With Original取消勾选
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-24-07.jpg">}}

{{< alert danger >}} 注意，如果物体的结构比较复杂或者不规则时，镜像时需要关掉Cut Geometry。因为勾选后maya会自动缝合，复杂的结构自动缝合时并不是预期的效果。{{< /alert >}}

官方文档：Mirror Settings  
https://knowledge.autodesk.com/support/maya-lt/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/MayaLT/files/GUID-E66AE3D8-3B9C-4D4E-9A3E-5BDAFCD67F1D-htm.html

##### Fill Hole
假设有这样一个模型，上面有个洞
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-25.jpg">}}
现在需要补洞，先选中洞的一条边（随便一条即可），然后点击Mesh -》 Fill Hole，或者按住shift键+鼠标右键 -》 Fill Hole，即可完成补洞。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-26.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-27.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-28.jpg">}}

##### Mesh Smooth
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-29.jpg">}}
一个正方体被Smooth之后的效果：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-30.jpg">}}

可以多次执行Smooth，执行次数越多则模型会圆滑：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-31.jpg">}}

##### Cleanup 清理
Cleanup可以帮我们检查并修复模型上不易察觉的问题，比如检测边数大于4的面。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-32.jpg">}}

点击Cleanup之后，就会弹出参数面板
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-33.jpg">}}

常用参数  
**Cleanup Effect**

+ Operation：两个选项，Cleanup matching polygons表示执行修复清理；Select matching polygons表示只选中有问题的多边形但不修复。
+ Scope：两个选项，Apply to selected objects表示只对选中的对象进行清理；Apply to all polygonal objects表示对所有对象执行清理。

**Fix by Tesselation**

+ 4-side faces
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-34.jpg">}}
+ Faces with more than 4 sides
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-35.jpg">}}
+ Concave faces
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-36.jpg">}}
+ Faces with holes
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-37.jpg">}}
+ Non-planar faces
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-38.jpg">}}

**Remove Geometry**

+ Lamina Faces  
比如有两个正方形的Plane，然后把这两个面的四个顶点两两合并（Merge Vertices），此时虽然表象看是一个平面了，但是实际还是存在两个重叠的面，此时就可以用Lamina Faces选项检测出这种重叠的面。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-39.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-40.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-41.jpg">}}

Cleanup详细参数的官方文档：  
https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/Maya/files/GUID-AB60C982-C96E-4947-8CF3-5152406B6A40-htm.html


##### Smooth保留硬边
平滑时默认会把有棱角的硬边软化掉。例如：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-42.jpg">}}
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-43.jpg">}}

如果希望平滑时保留棱角结构，在Smooth Options参数面板中选择Subdivision为Maya Catmull-Clark，勾选Hard Edges。
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-44.jpg">}}

这样再平滑一个正方体时，就不会把正方体的棱角软化，平滑后的效果如下：
{{< figure src="/img/20171002-[Maya]Mesh/[Maya]Mesh-45.jpg">}}

***
`争名者于朝，争利者于市。---《战国策》`