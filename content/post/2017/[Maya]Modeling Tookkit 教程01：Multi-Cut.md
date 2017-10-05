+++
title= "[Maya]Modeling Tookkit 教程01：Multi-Cut"
date= "2017-10-02T19:37:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018
点击右上角的Toolkit图标，打开Modeling Toolkit面板。
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-01.jpg">}}
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-02.jpg">}}

下面讲解Multi-Cut的用法。
先新建一个正方体
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-03.jpg">}}
然后点击Multi-Cut
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-04.jpg">}}

##### 绘制单条边线
光标悬停在模型的点或者边上，点和边会变成红色，表示可以绘制顶点
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-05.jpg">}}
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-06.jpg">}}

点击一下顶点或者边线，然后再在空白位置点一下，即可绘制新的顶点和边线：
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-07.jpg">}}

绘制过程中，起点和终点必须都在原有的模型得到边或者顶点上，如果终点还没有连接其他顶点或边线，则表示绘制还没结束，此时可以接着修改当前新顶点的位置：光标悬停在顶点上，顶点变成红色后，按住鼠标左键拖动。
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-08.jpg">}}

当终点连接顶点或者边线后，则可以完成这一次绘制，单击鼠标右键，表示绘制结束
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-09.jpg">}}
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-10.jpg">}}

##### 绘制环绕边线
光标悬停在某条边线，边线变红色，按住Ctrl键不放，此时会出现一条黄色的环绕边线
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-11.jpg">}}
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-12.jpg">}}

来回移动光标，该黄线会自动跟随光标移动，等确定位置后，单击下鼠标左键，即可绘制出一条环绕的边线。
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-13.jpg">}}

##### Snap Step （按住Shift键才生效）
Multi-Cut有个参数叫Snap Step，表示在卡边（绘制顶点和边线）时，光标可以自动吸附边线的均等份位置上，前提时按住Shift键。  
比如默认是10%，表示在按住shift键后，光标在边线上移动时，光标会自动吸附边线的最近的10等分点的位置，如果是50%，则表示光标每次会自动吸附在边线的中点位置。这个操作对上述的环线和单条线都适用。
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-14.jpg">}}

例如，Snap Step设置为50%后的效果
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-15.jpg">}}
{{< figure src="/img/20171002-[Maya]Modeling Tookkit 教程01：Multi-Cut/[Maya]Modeling Tookkit 教程01：Multi-Cut-16.jpg">}}



