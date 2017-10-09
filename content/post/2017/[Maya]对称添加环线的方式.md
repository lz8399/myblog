+++
title= "[Maya]对称添加环线的方式"
date= "2017-10-08T11:56:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

Keywords：Maya、Edge Loop

##### 方式1：Insert Edge Loop
点击菜单Mesh Tools -》 Insert Edge Loop菜单的小方框
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-01.jpg">}}

或者选中Edge并Shift+鼠标右键，点击Insert Edge Loop Tool
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-02.jpg">}}

打开属性面板后，Maintain position选择Multiple Edge Loops，然后需要对称环线的条数Number of edge loops。  
如果只是单条环线，Maintain position选择Relative distance from edge。
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-03.jpg">}}

如果Number of edge loops是偶数，则会在鼠标点击的位置的两旁分别创建环线
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-04.jpg">}}
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-05.jpg">}}

如果是奇数，则在鼠标的点击位置处会有一条环线
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-06.jpg">}}

这种方式创建的环线是固定在线段的均等处的，比如线条个数是3，那么每条线分别在边线的1/4等分点的位置。

##### 方式2：Offset Edge Loop Tool
先插入单条环线，
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-07.jpg">}}

然后shift + 右键选择Offset Edge Loop Tool
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-08.jpg">}}

然后在单条环线的位置处左右拖拽
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-09.jpg">}}
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-10.jpg">}}

注意，拖拽时的两条环线的位置是相对中间环线的上下间隔比例来移动的：如果中间环线正好在相交边线的正中间，那么两offset环线和中间的环线的间隔是等距的；如果中间环线靠下，那么两条offset环线与中间环线的间隔是不等距的。
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-11.jpg">}}
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-12.jpg">}}

##### 方式3：Bevel 倒角
先插入单条环线并选中
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-13.jpg">}}

然后点击Bevel（Ctrl+B或者Edit Mesh -》 Bevel），在Chanel box面板中修改offset和segments，前者表示间距，后者表示条数。
{{< figure src="/img/20171008-[Maya]对称添加环线的方式/[Maya]对称添加环线的方式-14.jpg">}}
