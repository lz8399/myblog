+++
title= "[Maya]Mesh Tools"
date= "2017-09-30T23:37:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

##### Create Polygon
Create Polygon作用是可以自由创建一个多边形。  
Shift + 鼠标右键 -》 Create Polygon Tool，或者点击菜单 Mesh Tool -》 Create Polygon（2018版本。Maya老版本的Create Polygon Tool 在Mesh菜单下）
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-01.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-02.jpg">}}

然后就在可以场景中，多次单击鼠标左键，画出自定义多边形。
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-03.jpg">}}

完成后再点击鼠标右键 -》 Complete Tool，或者点击Enter回车键，来完成一个自定义多边形的创建。
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-04.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-05.jpg">}}


##### Append to Polygon（相当于Bridge的DIY版本）
假设有两个正方体，两个对立面是开口的
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-06.jpg">}}
先将模型Combine（Mesh -》 Combine）
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-07.jpg">}}
然后点击 Mesh Tools -》 Append to Polygon
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-08.jpg">}}
此时开口的边会被自动加粗
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-09.jpg">}}
然后加粗的某一条边，这些边周围会显示紫色的线
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-10.jpg">}}
然后点击另外一条与之桥接的边，此时就会将两条边线桥接起来
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-11.jpg">}}
然后再按Y键，表示这两条边桥接完成，准备桥接其他边
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-12.jpg">}}
然后再点击其他的一条边，
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-13.jpg">}}
然后再点击与之桥接的另一条边
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-14.jpg">}}
重复这些步骤直至所有桥接的边完成。

##### Multi-Cut（快捷键Ctrl+shift+X，对应maya旧版本中的Cut Face Tool）
点击Mesh Tools -》 Multi-Cut，然后再按住鼠标左键不放拖动
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-15.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-16.jpg">}}

画好线以后在松开鼠标，就可以形成一条线，不在视线范围内的区域也会被划线
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-17.jpg">}}

如果想在指定区域划线，可以先选中面，然后再划线
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-18.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-19.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-20.jpg">}}

##### Insert Edge Loop
Mesh Tool -》 Insert Edge Loop，或者按住shift+ 鼠标右键-》 Insert Edge Loop Tool，其作用是画出一条环形的线。
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-21.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-22.jpg">}}

效果
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-23.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-24.jpg">}}

但是这条环线只穿越四角面，三角面和五角面则会让其终止。比如如下情形：
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-25.jpg">}}
{{< figure src="/img/20170930-[Maya]Mesh Tools/[Maya]Mesh Tools-26.jpg">}}