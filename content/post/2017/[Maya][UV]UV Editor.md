+++
title= "[Maya][UV]UV Editor"
date= "2017-10-31T12:23:40+08:00"
categories= ["Maya"]
tags= ["Modeling", "UV"]
keywords= ["Maya", "分UV", "展UV", "UV编辑器", "UV Editor"]
+++

Maya版本为2018.1

##### 打开UV编辑器
点击菜单：UV -》UV Editor
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-01.jpg">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-02.jpg">}}

##### 打开UV Toolkit
打开UV Editor的同时，会自动打开UV Toolkit面板
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-03.jpg">}}

##### UV Editor常用快捷菜单
面板顶部列出了常用的菜单
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-04.jpg">}}

最左边3个按钮分别是：边框显示、颜色块显示、扭曲度显示。前两个必须二选一，后面一个不是必选。
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-05.png">}}

+ 边框显示（Wireframe）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-06.png">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-07.jpg">}}
+ 颜色块显示（Shaded）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-08.png">}}
正向法线的面显示为蓝色，反向法线的面显示为红色
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-09.jpg">}}
也可以Shift+鼠标左键单击按钮，打开设置菜单，来设置正向和反向的颜色
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-10.jpg">}}
如果右键单击改按钮，则每个UV壳以不同颜色显示
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-11.jpg">}}
+ 扭曲度/畸变度显示（UV Distortion）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-12.png">}}
扭曲程度越严重，则红色越深，平铺越均匀则白色越深。
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-13.jpg">}}
+ 显示贴图边框（Texture Borders）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-14.png">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-15.jpg">}}
+ UV壳边界显示（Shell Borders）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-16.png">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-17.jpg">}}
+ 关闭/显示UV网格（Grid）
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-18.png">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-19.jpg">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-20.jpg">}}
+ UV贴图输出
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-21.png">}}
UV贴图制作完成后输出到指定路径
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-22.jpg">}}

##### Pin Selection 锁定
如果想锁定UV的顶点，让其不可编辑，则选中需要锁定的顶点或者UV壳，然后点击UV Editor中的：Edit -》 Pin Selection。被锁定的区域会被表示为蓝色。
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-23.jpg">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-24.jpg">}}
如果要取消锁定，再点击：Edit -》 Unpin Selection。

##### Check Map 棋盘格检查UV
打开棋盘格之后可以检测UV的拉伸畸变是否严重
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-25.jpg">}}
{{< figure src="/img/20171031-[Maya][UV]UV Editor/[Maya][UV]UV Editor-26.jpg">}}

***
`前事不忘，后事之师。---《战国策》`
