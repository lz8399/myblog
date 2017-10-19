---
title: "[ZBrush]ZModeler常用操作示例-01"
date: "2017-07-30T15:31:42+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
--- 

Keyword：zbrush、zmodeler

##### Initialize用法
新建一个圆柱体
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-01.jpg">}}

其默认Initialize参数如下（Tool -》 Initialize）
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-02.jpg">}}

如果想减掉模型纵向的polygon数量，则可以将VDivide修改4（对于圆柱体，可修改的最小值也只能是4，表示纵向方向上用4根横向的线分段），默认为17。比如纵向的网格数量修改为3，则修改VDivide为4：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-03.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-04.jpg">}}

如果想减掉模型横向的polygon数量，则可以修改HDivide。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-05.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-06.jpg">}}


##### Move（将所在面压低或抬高）
<font color=red>注意，使用ZModeler之前，需要将模型转换为PolyMesh3D。</font>  
先将鼠标悬停在需要压扁面上，注意，是面上，不是边也不是点，鼠标悬停的位置不同，相应的弹出菜单也不同。  
然后按住空格键不放，弹出菜单中，Action选择Move，Target选择Flat Island。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-07.jpg">}}

然后可以鼠标悬停在面上，按住鼠标不放，上下移动来压扁或者拉长模型
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-08.jpg">}}

##### Inset（Island内插入）
比如我们想在上面示例的圆柱截面上，插入一根线，效果如下：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-09.jpg">}}

方式：先将鼠标悬停在面上，按住空格键不放，弹出菜单中，Action选择Inset、Target选择Flat Island、Modifiers选择Inset Region
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-10.jpg">}}

<font color=red>注意：鼠标要悬停在面上且出现一根黄线后再拖动，否则就是另外一种效果。</font>  
未出现黄线：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-10-1.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-10-2.jpg">}}
出现黄线：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-10-3.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-10-4.jpg">}}
##### Inset（Polygroup内插入）
如果想在一个某个Polygroup内部插入，则将Target选择为Polygroup Island，否则每次只能从圆柱体截面的最外面插入。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-11.jpg">}}

效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-12.jpg">}}

##### Move（Polygroup压扁或拉伸）
如果想把某块Polygroup抬高或者压低，同样使用Move，只是把Target选择为Polygroup Island。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-13.jpg">}}

效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-14.jpg">}}

##### QMesh（以所在面为基础，挤压出新的部位出来）
接着上面案例，actions选择QMesh、Target选择Polygroup Island
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-15.jpg">}}

向上挤压效果效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-16.jpg">}}

向下挤压效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-17.jpg">}}

##### Scale（伸缩）
比如，想把下面模型的顶部圆形扩大或缩小
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-18.jpg">}}

方式1：面级别的Scale
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-19.jpg">}}

方式2：线级别的Scale
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-20.jpg">}}

效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-21.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-22.jpg">}}

##### Bevel（倒角）
一个模型的棱角如果不卡边，比如这样：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-23.jpg">}}

那么执行Dynamic（Tool -》 Geometry -》 Dynamic Subdiv -》 Dynamic）后的效果就成了这样：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-24.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-25.jpg">}}

ZModeler的卡边方式：鼠标悬停在线上，Edge Actions选择Bevel，Target选择EdgeLoop Complete。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-26.jpg">}}

然后在需要卡边的线上按住鼠标左键拖拽：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-27.jpg">}}

以此案例为例，如果圆柱底部的边也需要做同样的卡边，直接单击底部的边线即可：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-28.jpg">}}

之后再执行Dynamic，棱角就不会被过度平滑：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-29.jpg">}}

Bevel另外一种常用方式是，将Modifiers选择为Two Rows，如果觉得两条不够，还可以选择Four Rows、Eight Rows。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-30.jpg">}}

比如这种案例
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-31.jpg">}}

执行卡边的时候就会自动生成两条edge：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-32.jpg">}}

##### Insert（插入）
再介绍一种和Bevel效果类似的方法，鼠标悬停在线上，Edge Actions选择Insert，Target选择Single EdgeLoop。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-33.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-34.jpg">}}

然后再执行Dynamic：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-35.jpg">}}

##### Inset和QMesh综合使用：制作套环
比如想制作如下效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-36.jpg">}}

方式如下：鼠标先悬停在面上，按住空格键，Polygon选择Inset，Target选择Polyloop，Modifiers选择Inset Region
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-37.jpg">}}

然后鼠标悬停在polygon上，左右晃动，会出现两种黄线，一种纵向，一种横线：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-38.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-39.jpg">}}

这里我们需要的是横向上的polyloop，所以等显示横向黄线时，按住鼠标拖拽，即可形成一段polyloop：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-40.jpg">}}

然后再选择QMesh，在这个polyloop上按住鼠标左键拖拽，即可创建出套环效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-41.jpg">}}

##### Delete（删除）
以下图模型为例
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-42.jpg">}}

鼠标悬停在线条上，空格键按住不放，然后选Action选择Delete、Target选择EdgeLoop Complete：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-43.jpg">}}

然后点击需要删除的边：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-44.jpg">}}

效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-45.jpg">}}

#### 其他技巧：
##### 1，QMesh复制与隔离
前面说到，使用QMesh可以从一个Polygroup挤出一块，如果不想挤出，只是希望将选中的Polygroup复制一份出来并抬高，且与之前的模型隔离开，比如这种效果：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-46.jpg">}}

方式：按住鼠标不放之后，拖拽鼠标之前，按住Ctrl键。

##### 2，Move继续操作
比如已经move一次，然后再move一次时，会看到多出来一条线，效果如下：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-47.jpg">}}

如果想接着上次的Move，继续Move，比如这样：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-48.jpg">}}

方式：在按住鼠标不放之后，拖拽鼠标之前，按住Shift键。

##### 3，Insert Multiple EdgeLoops
鼠标悬停在线条上，按住空格，Action选择Insert，Target选择Multiple EdgeLoops，那么之后每此在Edge上点击一次，zb就会自动在线条的中点位置创建一条edgeloop。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-49.jpg">}}

执行前：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-50.jpg">}}

执行后：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-51.jpg">}}

如果在线条上拖拽，则会自动生成Polygroup：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-52.jpg">}}

拖拽的距离越长，生成的polygroup越多，且距离也是等分的。
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-53.jpg">}}


##### 注意事项：
加入圆柱行上下两个截面的布线结构有差异，比如下图中，左边截面上多一条edge，右边没有edge：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-54.jpg">}}
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-55.jpg">}}
那么执行Dynamic后的效果，左右两边棱角结构也会有差异：
{{< figure src="/img/20170731-[ZBrush]ZModeler常用操作示例/[ZBrush]ZModeler常用操作示例-56.jpg">}}

要解决这个问题，可以在Dynamic之前，在右面的对应位置，加上一条edge。

##### 其他参考
Polygon各个Actions的用法：  
http://docs.pixologic.com/user-guide/3d-modeling/modeling-basics/creating-meshes/zmodeler/zmodeler-actions/polygon-actions/
