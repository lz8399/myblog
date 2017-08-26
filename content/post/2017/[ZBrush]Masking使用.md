---
title: "[ZBrush]Masking使用"
date: "2017-01-18T21:28:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keyword：Masking，MaskPen，蒙板

##### mask笔刷有六种：
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-01.jpg">}}

按住Crtl键，默认打开MashPen。
此时既可以在模型上直接画，也可以在空白区域拉出一个矩形，被框选的范围就成了蒙板。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-02.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-03.jpg">}}


画出蒙板后，再按Ctrl + W，可以将模版区域变成PolyGroups。

##### Mask反选
Tool -》 Masking -》 Inverse。快捷键Ctrl + I。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-04.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-05.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-06.jpg">}}

##### 取消mask
在模型之外的空白区域，点击：Ctrl + 鼠标左键

##### Mask的羽化与锐化
原始mask：
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-07.jpg">}}

羽化：按住Ctrl键，在模型上点击一下鼠标左键。可以多次点击，点击的次数越多，羽化效果越微弱
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-08.jpg">}}

锐化：按住Ctrl + Alt，再在模型上点击一下鼠标左键。 可以多次点击，点击次数越多，锐化越强烈。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-09.jpg">}}

##### Auto Masking
当模型有PolyGroup后，再点击Brush -》 Auto Making -》 Mask By Polygroups的值改大一些，之后在使用普通brush时，就可以过滤Polygroups的范围区域。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-10.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-11.jpg">}}


当笔刷从哪个蒙板开始画时，那么该笔刷的所有区域只能限定在改蒙板内。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-12.jpg">}}

##### 结合Polygroups中的用法
假如有4个分组过的模型，在Move模式下移动时，默认是4个模型一起移动的。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-13.jpg">}}

如果将Mask By Polygroups改成100，那么move时，move线是从哪个模型中拉出来的，那么该move线只对该模型进行移动。


##### BackfaceMask用法
对于很薄的面，在其上面雕刻时，默认情况下会同时影响正面和反面
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-14.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-15.jpg">}}

如果只想对当前雕刻的那一面起作用，打开：Brush -》 Auto Masking -》 BackfaceMask。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-16.jpg">}}

##### Group Masking
**反选**  
如下图，两个Group，一个被Mask了，一个没有Mask。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-17.jpg">}}
如果想反向Mask，即：没有被Mask的Group被Mask，被Mask的Group取消Mask。可以在空白区域点击以下鼠标，即可完成切换。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-18.jpg">}}

**取消**  
如果要取消所有的Mask，可以在空白区域拖拽以下鼠标。
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-19.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-20.jpg">}}

**Mask时排除单个Group**  
如果所有Group都没有被Mask，希望将某个Group之外的所有Group都Mask，可以先打开Move模式（W键）
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-21.jpg">}}
然后单击以下想要不被Mask的Group
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-22.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-23.jpg">}}

**全选**  
按住Ctrl键，框选所有Group
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-24.jpg">}}

##### 单面Masking
默认情况下，两个间隔距离非常近的面，如果对其中一个进行mask，则对面的mask也会被mask
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-25.jpg">}}
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-26.jpg">}}

如果希望mask的时候，背对的面不被mask，点击：Brush -》 AutoMasking -》 BackFaceMask。  
<font color=red>注意：点击的时候按住Ctrl键，表示对Mask笔刷生效。点击的时候选择的是哪个笔刷，则对哪个笔刷生效。</font>
{{< figure src="/img/20170118-[ZBrush]Masking使用/[ZBrush]Masking使用-27.jpg">}}

