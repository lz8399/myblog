+++
title= "[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)"
date= "2017-11-13T22:41:40+08:00"
categories= ["Map-Baking"]
tags= ["Map-Baking", "Maya"]
keywords= ["Maya", "Color ID Maps", "Diffuse Maps", "颜色贴图", "ID贴图"]
+++

Keywords：Maya、Color ID Maps/Diffuse Maps 颜色贴图/ID贴图

Maya版本为2018.1

##### 1，准备好低模、低模UV、高模。
假设我们已经做好了低模和高模
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-01.jpg">}}
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-02.jpg">}}

并且假设我们已经为低模做好了UV
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-03.jpg">}}

##### 2，编辑Shader材质
打开Hypershade窗口：点击Windows -》 Rendering Editors -》 Hypershade。设置shader材质
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-04.jpg">}}

首次打开后，默认只有3种材质(Material)
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-05.jpg">}}

这里我自定义了红绿蓝三种颜色的材质
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-06.jpg">}}

##### 3，使用shader材质给高模着色
在模型中选中需要上色的面
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-07.jpg">}}

然后再在材质栏中右键单击需要上色的材质 -》 Assign Material To Selection。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-08.jpg">}}

这样选中的面就会被涂上指定的颜色材质。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-09.jpg">}}

当前示例使用了3种颜色，最终效果如下：
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-10.jpg">}}
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-11.jpg">}}

##### 4，Transfer Maps窗口，设置参数并烘焙
上好颜色后，在切换到Rendering模式
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-12.jpg">}}

再点击菜单：Lighting/Shading -》 Transfer Maps。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-13.jpg">}}

打开后记得先点击Target Meshes和Source Meshes的Clear All，以清除旧的历史记录。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-14.jpg">}}

然后在Target Meshes中选中低模并Add，在Source Meshes中选中高模并Add。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-15.jpg">}}
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-16.jpg">}}

然后点击一下Diffuse，表示输出一张color ID贴图，格式我们选择PNG。点击一次后以后再次打开Transfer Maps版本就会默认保留这个输出选项，不需要再点击。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-17.jpg">}}

其他的常用修改参数为贴图尺寸、抗锯齿级别。
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-18.jpg">}}

最后点击Bake，就可以生成color ID贴图。当前示例的贴图效果：
{{< figure src="/img/20171113-[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)/[Map-Baking]Maya烘焙ID贴图(ID Color Maps、Diffuse Maps)-19.jpg">}}

{{< alert danger>}}
烘焙贴图时（包括ID、法线等），一定要保证高模没有UV，如果有UV一定要删掉，高模低模同时有UV时，即使两个UV的轮廓一模一样，烘焙贴图时也会耗时很长。以ID贴图烘焙为例，如果高模没有UV，可以瞬间完成。
{{< /alert >}}

