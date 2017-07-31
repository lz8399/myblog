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

keyword：zbrush、Customize UI、Interface Layout、Menu Button

##### 设置button大小
安装zb后，默认的按钮宽度是44，效果如图：
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-01.jpg">}}

如果想让菜单布局更紧凑，缩短button的宽度，可以作如下修改：  
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
如果要删除界面上的菜单按钮，同样按住Ctrl + Alt键不放，鼠标左键点击笔刷菜单并按住不放，将菜单拖拽到视图界面中（就是编辑模型的主视图）或者该按钮不可放置的区域中。


##### 还原UI布局
如果不小心删除了某个菜单按钮，或者想还原为默认设置，可以点击：  
Preferences -》 Config -》 Restore Custom UI或者Restore Standard UI，前者是自己上次保存的UI布局，后者是系统的初始UI布局。
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-07.jpg">}}

##### 如何将新笔刷加入Quick Pick面板
以TrimSmoothBorder为例，这是zb自带的笔刷，但是不在Quick Pick面板钟，而是在Pixologic\ZBrush 4R7\ZBrushes\Trim\目录下
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-08.jpg">}}

先将TrimSmoothBorder.zbp拷贝到Pixologic\ZBrush 4R7\ZStartup\BrushPresets\目录下
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-09.jpg">}}
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-10.jpg">}}

然后重启zb，再次打开quick pich，就可以在末尾看到新加入的笔刷
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-11.jpg">}}

这个使用就可以选择一次该笔刷后，在Brush菜单下看到最近使用的历史笔刷，然后就可以按住Ctrl+Alt键来拖抓到快捷栏中
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-12.jpg">}}
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-13.jpg">}}

##### 如何保存UI布局
点击Preferences -》 Config -》Store Config，表示将当前UI设置保存zb的默认设置，也就是说以后每次启动就使用这个设置。Save UI表示导出当前UI布局的配置文件。
{{< figure src="/img/20170702-[ZBrush]自定义菜单布局(Custom Interface Layout)/[ZBrush]自定义菜单布局(Custom Interface Layout)-14.jpg">}}

其他参考文档：  
CUSTOM INTERFACE  
http://docs.pixologic.com/user-guide/customizing-zbrush/interface-layout/custom-interface/

视频教程：  
Zbrush Customize UI  
https://www.youtube.com/watch?v=Jr3XNnctUfI