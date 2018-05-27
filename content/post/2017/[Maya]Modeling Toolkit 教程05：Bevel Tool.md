+++
title= "[Maya]Modeling Toolkit 教程05：Bevel Tool"
date= "2017-10-06T09:58:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018

先选中要倒角的边
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-01.jpg">}}


然后点击Bevel
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-02.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-03.jpg">}}

如果想在倒角时设置更多的参数，可以按住Shift键再点击Bevel按钮，就可以弹出参数菜单。
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-04.jpg">}}

##### 倒角大小设置
倒角的大小有参数Fraction控制，默认是0.5（边线的二分之一处），如果改成0.1（边线的十分之一处）则倒角会变小
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-05.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-06.jpg">}}

也可以把Offset as Fraction关掉，通过Offset来设置倒角的大小，效果一样。
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-07.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-08.jpg">}}

##### Segments 倒角密度
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-08-02.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-08-03.jpg">}}

##### Depth 倒角方向
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-09.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-10.jpg">}}
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-11.jpg">}}


##### Bevel的Hotbox
选中Edge后，Shift按住不放+鼠标右键
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-12.jpg">}}

##### Bevel处理棱角的三种效果
假设一个正方体，准备对其三条边线进行倒角
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-13.jpg">}}
分3中情况：

+ 1，选中三条边同时倒角。这样棱角就是一个三角形
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-14.jpg">}}
+ 2，三条边线逐个倒角。
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-15.jpg">}}
+ 3，先选中两条边进行倒角，然后再对第三条倒角。这样棱角就是一个正方形
{{< figure src="/img/20171006-[Maya]Modeling Tookkit 教程05：Bevel Tool/[Maya]Modeling Tookkit 教程05：Bevel Tool-16.jpg">}}

{{< alert danger >}} 不建议用第二种和第三种，因为这样会产生五边面，结构复杂了以后要处理很多五边面、六边面。 {{< /alert >}}

##### polyBevel官方文档  
https://knowledge.autodesk.com/support/maya/learn-explore/caas/CloudHelp/cloudhelp/2018/ENU/Maya-Modeling/files/GUID-40E32F44-1EB9-4DC6-8EE4-6A013EEC626F-htm.html

***
`一场消黯，永日无言，却下层楼。---柳永《曲玉管》`