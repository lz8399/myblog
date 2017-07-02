---
title: "[ZBrush]自定义菜单布局(Custom Interface Layout)"
date: "2017-07-02T17:20:42+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
--- 

##### 设置button大小
安装zb后，默认的按钮宽度是44，效果如图：
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-01.jpg">}}

如果想让菜单布局更紧凑，缩短button的宽度，可以坐如下修改：  
Perferences -》 Interface -》 UI -》 修改Buttons Size，或者取消Wide Buttons
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-02.jpg">}}

取消Wide Buttons之后的效果
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-03.jpg">}}

##### 移动菜单按钮的位置
先启用自定义UI选项：Preferences -》 Config -》 Enable Customize
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-04.jpg">}}

这里以移动常用笔刷到底部菜单栏为例。  
点击Brush，找到需要的笔刷，然后按住Ctrl + Alt键不放，鼠标左键点击笔刷菜单并按住不放，拖拽到底部的Shelf上
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-05.jpg">}}

最后效果：
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-06.jpg">}}

##### 按钮删除
如果要删除界面上的菜单按钮，同样按住Ctrl + Alt键不放，鼠标左键点击笔刷菜单并按住不放，将菜单拖拽到视图界面中（就是编辑模型的主视图）或者该按钮不可防止的区域中。


##### 还原UI布局
如果不小心删除了某个菜单按钮，或者想还原为默认设置，可以点击：  
Preferences -》 Config -》 Restore Custom UI或者Restore Standard UI，前者是自己上次保存的UI布局，后者是系统的初始UI布局。


其他参考文档：  
CUSTOM INTERFACE  
http://docs.pixologic.com/user-guide/customizing-zbrush/interface-layout/custom-interface/