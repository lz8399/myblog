+++
title= "[Next-Gen]锈迹材质全流程实例：Blender-》SP-》UE4"
date= "2018-03-21T01:55:02+08:00"
categories= ["Next-Gen"]
tags= ["Material", "Blender", "SubstancePainter", "UE4"]
+++

##### 1，准备Mesh
准备一个现成模型资源。这里从Blender中提取现成的猴头模型

按住Shift + A -》 Mesh -》 Monkey
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-01.jpg">}}
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-02.jpg">}}

自动生成UV
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-03.jpg">}}

然后执行Smooth
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-04.jpg">}}

然后增加细分级别
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-05.jpg">}}

最终效果：
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-06.jpg">}}

##### 2，导出FBX
File -》 Export -》 FBX
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-07.jpg">}}

导出选项中勾选Select Objects。
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-08.jpg">}}

##### 3，导入SP
File -》 New，打开创建工程界面，设置Mesh的FBX文件位置（刚刚导出的FBX），其他不用修改。
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-09.jpg">}}

因为当前示例中的AO、Normal等等贴图我们会在SP中自动生成，所以这里“Import Mesh NOrmal Map ...”中可以不添加任何东西，如果你的模型已经有现成的贴图，可以在这里Add。

点击OK，在SP中可以看到默认贴图和UV
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-10.jpg">}}
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-11.jpg">}}

##### 4，烘焙贴图
在Layer面板中，点击 Bake Textures，打开烘焙选项面板
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-12.jpg">}}

不勾选ID，并设置贴图大小
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-13.jpg">}}

点击Bake DefaultMaterial Textures，稍等一会后，就可以在Project中看到6张贴图
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-14.jpg">}}

##### 5，编辑材质
打开Smart Materials
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-15.jpg">}}

选一个要想材质，这里我选择的是Steel Rust Surface
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-16.jpg">}}

然后拖拽到Layer面板钟
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-17.jpg">}}

立即可以看到效果
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-18.jpg">}}

同时，在TextureSet Settings中可以看到自动帮我们设置好了前面烘焙好的各种贴图
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-19.jpg">}}

SP提供的智能材质很多，这些材质帮你省去了手动调参数的步骤，相当于材质模版。材质里面的具体参数我没深究过，所以我也不详细讲各种参数的使用了，这些参数具体可以看SP官方视频或文档。


其他两种智能材质效果
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-20.jpg">}}
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-21.jpg">}}


##### 6，导出贴图
右键贴图 -》 Export Textures
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-22.jpg">}}

Config选择UE4 -》勾选DefaultMaterial -》 Export
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-23.jpg">}}

最终的输出图片（因为当前示例中没有用到自发光，所以没有输出Emissive贴图）
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-24.jpg">}}

##### 7，导入UE4
先倒入模型FBX
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-25.jpg">}}

导入选项面板默认即可 -》 Import。
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-26.jpg">}}

然后，在拖拽到场景中
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-27.jpg">}}

然后新建Material
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-28.jpg">}}

然后导入贴图
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-29.jpg">}}

打开Material蓝图，如下编辑材质
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-30.jpg">}}

OcclusionRoughnessMetallic贴图的红色通道连AO（环境光）、绿色通道连Roughness（粗燥度）、蓝色通道连Metallic（金属度），其他两张贴图用混合通道连对应名称。


材质球效果
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-31.jpg">}}

然后将材质球拖拽到模型上
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-32.jpg">}}

最终效果
{{< figure src="/img/20180320-[Material]锈迹材质全流程实例：Blender-》SP-》UE4/[Material]锈迹材质全流程实例：Blender-》SP-》UE4-33.jpg">}}

头顶颜色泛蓝是因为场景中有个天空盒，反射效果。