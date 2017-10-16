+++
title= "[Maya]Lighting & Shading"
date= "2017-10-08T23:14:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

Maya版本为2018


##### Assign Material
Maya新建物体后，默认是没有材质效果的，如果想看下简单的渲染效果，可以切换到Rendering模式下，点击Lighting/Shading -》 Assign Existing Material -》 选择需要的材质。
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-01.jpg">}}

快捷方式是右键点击物体，选择Assign Existing Material，然后选择材质
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-02.jpg">}}

左边为默认着色效果，右边为Blinn材质的着色效果。
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-03.jpg">}}

##### Two Sided Lighting
默认情况下，如果删除了模型的某个面，则其内部的面会显示为黑色，这样的好处是可以观察法线方向。
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-04.jpg">}}

如果希望内部的面也像正常面一样显示为灰色，则点击Lighting -》 Two Sided Lighting
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-05.jpg">}}
{{< figure src="/img/20171008-[Maya]Lighting & Shading/[Maya]Lighting & Shading-06.jpg">}}
但是不建议这样做，因为这样做出来的模型倒入引擎后，模型会显示为半透明，当然在引擎中可以调整贴图属性来修复模型透明的问题，比如在UE4中可以通过Blend Mode属性，但是这种搞法终究不正规。

