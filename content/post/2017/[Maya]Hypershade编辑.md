+++
title= "[Maya]Hypershade编辑"
date= "2017-11-16T15:45:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
keywords= ["Maya", "Hypershader"]
+++

Maya版本为2018

Hypershade是Maya中编辑shader材质的工具，比如制作ID贴图时会用到Hypershader。

##### 打开Hypershade窗口
点击Windows -》 Rendering Editors -》 Hypershade。设置shader材质
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-01.jpg">}}

首次打开后，默认只有3种材质(Material)
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-02.jpg">}}

##### 编辑Shader材质
要创建自定义颜色的材质，先在Create面板中找到需要的材质模板，单击一下即可在Material栏中创建一个。这里我们使用Lambert这种默认材质。
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-03.jpg">}}
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-04.jpg">}}

选中材质后，再在中间的材质编辑栏中选中主体属性框
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-05.jpg">}}

然后再在右边的Property Editor中单击Color属性，打开取色器。
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-06.jpg">}}

然后选择需要的颜色。这里择取红色
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-07.jpg">}}

然后就可以将自定义材质设置为指定的颜色。
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-08.jpg">}}

##### 用途：给模型着色
在模型中选中需要上色的面
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-09.jpg">}}

然后再在材质栏中右键单击需要上色的材质 -》 Assign Material To Selection。
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-10.jpg">}}

这样选中的面就会被涂上指定的颜色材质。
{{< figure src="/img/20171116-[Maya]Hypershade编辑/[Maya]Hypershade编辑-11.jpg">}}

***
`人之有德于我也，不可忘也；吾有德于人也，不可不忘也。---《战国策》`