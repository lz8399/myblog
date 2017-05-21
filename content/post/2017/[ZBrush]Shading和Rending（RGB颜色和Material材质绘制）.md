---
title: "[ZBrush]Shading和Rending（RGB颜色和Material材质绘制）"
date: "2017-05-20T21:14:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---


Keywords：RGB、MRGB、Vertex Shading、Rending、顶点着色、UV、Material、材质

ZBrush提供了直接在模型表面绘制颜色和材质的功能。  
优点：这样可以快速出渲染效果。如果用标准的次时代流程，涉及到分UV、贴图制作，周期较长。  
缺点：zb上直接制作出来的材质，无法导入第三方图形引擎中，只能用zb查看效果。

##### 绘制准备工作
1，将模型的材质换成：SkinShade4，这个材质方便观察绘制的颜色效果
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-01.jpg">}}
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-02.jpg">}}

2，打开模型的画笔功能，在Tool -》 SubTool下：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-03.jpg">}}

3，关掉Alpha：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-04.jpg">}}

4，固话所有Layer。因为着色时不能有Layer：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-05.jpg">}}

5，关掉Zadd，打开Rgb ：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-06.jpg">}}

参数说明

* MRGB：材质和颜色同时绘制。
* RGB：绘制颜色。
* M：绘制材质。
* RGB Intensity：是用来控制颜色的透明度。

6，在颜色面板中选择颜色，然后就可以绘画了
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-07.jpg">}}
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-08.jpg">}}

7，绘制过程中，可以选择Render的模式，来观察不同状态的效果：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-09.jpg">}}

* Best：效果最贴近真实渲染效果，但是相应速度较慢。
* Preview：渲染效果比Best差一点，但是速度快一点。
* Fast：去掉了灯光，速度更快，但是效果就差很多。
* Flat：隐藏掉了了模型的纹理，已纯平表面来显示绘制的效果，适合来观察颜色涂抹的均匀程度。

四中模式的效果依次是：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-10.jpg">}}

{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-11.jpg">}}

{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-12.jpg">}}

{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-13.jpg">}}

##### 颜色填充
点击Color，在取色器中选择要填充的颜色，然后点击 FillObject，就可以填充颜色
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-14.jpg">}}

填充颜色的强度，取决与RGB笔刷的强度Intensity
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-15.jpg">}}

填充效果示例：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-16.jpg">}}

##### 材质绘制
1，材质填充
先切换M模式，然后点击Color -》 FillObject，
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-17.jpg">}}

<font color=red>填充材质之后，再改变材质球，材质效果不会有任何变化</font>。

2，材质绘制
填充初始材质之后，就可以选中不同材质才绘制材质，这里选取红蜡材质Wax演示效果：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-18.jpg">}}

红蜡材质绘制的最终效果：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-19.jpg">}}

##### 渲染
材质调好以后，点击右上角的BPR，就可以渲染了
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-20.jpg">}}

渲染效果
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-21.jpg">}}

如果想调整不同材质之间的过渡渐变效果，修改：Render -》 Materials Blend-Radius。
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-22.jpg">}}

这是将Materials Blend-Radius修改30的渲染效果：
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-23.jpg">}}

##### 材质效果清除
比如上面绘制的材质效果不想要了，想还原到初始材质。步骤如下：
1，颜色模式切换到MRGB，并将Intensity调整为100。
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-24.jpg">}}

2，然后在Color面板中选择白色，然后再点击FillObject
1，颜色模式切换到MRGB，并将Intensity调整为100。
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-25.jpg">}}

这样模型材质就会还原到最初效果
1，颜色模式切换到MRGB，并将Intensity调整为100。
{{< figure src="/img/20170520-[ZBrush]Shading和Rending（RGB颜色和Material绘制）/[ZBrush]Shading和Rending（RGB颜色和Material绘制）-26.jpg">}}
