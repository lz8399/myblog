+++
title= "[Maya][UV]展UV完整流程实例"
date= "2017-11-03T19:55:40+08:00"
categories= ["Maya"]
tags= ["Modeling", "UV"]
keywords= ["Maya", "分UV", "展UV", "实例", "流程"]
+++

Maya版本为2018.1

{{< alert danger >}}
注意事项：分UV一定是用低模，而不是高模。若用高模来分UV，裁切时比较复杂，且不好优化。
{{< /alert >}}

假设分UV的模型如下，现在对其展UV。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-01.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-02.jpg">}}

步骤如下：
打开UV编辑器  
点击菜单：UV -》 UV Editor。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-03.jpg">}}

如果模型的结构较复杂，打开UV编辑器后，默认是空白的
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-04.jpg">}}

如果是一个简单结构的模型，maya会自动帮你展开UV，例如：
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-05.jpg">}}

**{{< hl-text blue >}} 自动分UV {{< /hl-text >}}**  
在UV Toolkit面板钟点击Create，选择需要创建的规则。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-06.jpg">}}

+ Automatic：自动创建
+ Planar：基于平面创建
+ Camera-Based：基于摄像机视角创建

当前示例中，自动创建的UV如下：
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-07.jpg">}}

**{{< hl-text blue >}} 手动分UV {{< /hl-text >}}**  
当结构较为复杂时，自动布局不是很合理，我们手工裁切，步骤如下：

##### 1，基于摄像机创建UV
先将摄像机调整为一个随意的方向，然后执行UV Toolkit面板钟的Create -》 Camera-Based，创建一个顶视图的UV布局。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-08.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-09.jpg">}}

##### 2，裁切UV壳
先将圆柱的上下两个圆的边框选中
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-10.jpg">}}

然后执行UV Toolkit面板中的Cut and Sew-》 Cut。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-11.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-12.jpg">}}

然后再将圆柱曲面切开：随便选中一条纵向的边线，然后再执行：Cut and Sew-》 Cut。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-13.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-14.jpg">}}

##### 3，展开UV并优化
先框选整个圆柱体
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-15.jpg">}}

然后执行UV Toolkit面板中的：Unfold -》 Unfold
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-16.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-17.jpg">}}

如果默认开后的UV壳比较弯曲，希望能够自动变直，则可以多次执行：Unfold -》 Optimize，来进行优化。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-18.jpg">}}

因为当前的结构比较简单，默认有没弯曲的UV壳，所以这里可以不用做优化。

##### 4，调整UV壳的旋转方向和大小
默认开后后，矩形的UV壳的选装方向是倾斜的，我们希望可以将其旋转为水平方向。  
先点击UV shell选中图标，表示切换到UV壳选中模式
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-19.jpg">}}

然后选中矩形UV壳，再按下W键，切换到旋转模式，条调整方向
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-20.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-21.jpg">}}

然后再按R键，切换到缩放模式，将UV壳缩小，让UV壳可以容纳在一单位长度的UV贴图内。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-22.jpg">}}

同样操作，再对圆形区域进行缩放
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-23.jpg">}}

##### 5，UV壳布局排列
缩放后以后，然在选中所有UV壳，然后执行：Arrange and Layout -》 Layout，maya就会自动将这些UV壳进行纵向或者横向排列，并自动调整UV壳的缩放，以填满一单位长度的UV区域。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-24.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-25.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-26.jpg">}}

到此，UV就分好了。

##### 6，检测贴图拉伸（棋盘格）
点击UV编辑器中的Textures -》 Checker Map，来检测UV拉伸是否严重
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-27.jpg">}}
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-28.jpg">}}

如果有的部位拉伸比较严重，则应该考虑将这部分区域切割成一个单独的UV壳，然后再展开。当然切割UV会产生新的接缝，如果没有比较隐蔽的位置适合做接缝，就得看项目的具体需求，是拉伸问题重要，还是贴图接缝问题重要。

比如可以将圆柱两个圆面的UV拆开：Cut and Sew -》 Cut。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-29.jpg">}}

然后再展开优化：Unfold -》 Optimize。  
这时的拉伸程度相比之前要好一些
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-30.jpg">}}

##### 7，导出UV
确定UV分好以后，就可以导出UV。  
点击UV Editor顶部的照相机按钮
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-31.jpg">}}

弹出面板中设置相应参数，比如贴图格式（通用格式是PNG），贴图大小、是否抗锯齿等等。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-32.jpg">}}

然后点击Apply，就会自动在指定路径名下面生成UV贴图，然后就可以扔到SP或DDO等材质工具中使用。
{{< figure src="/img/20171103-[Maya][UV]展UV完整流程实例/[Maya][UV]展UV完整流程实例-33.jpg">}}