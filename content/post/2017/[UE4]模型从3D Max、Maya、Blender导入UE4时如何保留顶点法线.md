+++
title= "[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线"
date= "2017-11-18T23:36:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "FBX", "Maya", "3D Max", "Blender", "Vertices Normals", "顶点法线", "Soften Edges", "Harden Edges"]
+++

keywords：UE4、FBX、Maya、3D Max、Blender、Vertices Normals、顶点法线、Soften Edges、Harden Edges

顶点法线在Max中叫做光滑组（Smoothing Group），在Maya中叫软硬边（Soften Edges/Harden Edges），Blender中叫光滑边（Smoothing Edge）。

#### 3D Max
##### FBX
{{< figure src="/img/20171119-[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线/[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线-01.jpg">}}

##### OBJ
{{< figure src="/img/20171119-[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线/[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线-02.jpg">}}

#### Maya
Maya无论导出FBX还是OBJ，都不需要在参数面板中勾选（根本就没有参数面板。。），导出时会默认保留对象上的软边和硬边。如果模型上有软边但又不希望导出，那么在导出前将这些边改成硬边。

#### Blender
##### FBX
{{< figure src="/img/20171119-[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线/[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线-03.jpg">}}

##### OBJ
{{< figure src="/img/20171119-[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线/[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线-04.jpg">}}

#### 导入游戏引擎
##### UE4
UE4导入资源的面板参数中，Normal Import Method表示是否使用资源自带的法线，默认是使用资源自带的（Import Normals）。
{{< figure src="/img/20171119-[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线/[UE4]模型从3D Max、Maya、Blender导入UE4时如何保留顶点法线-05.jpg">}}

##### Unity3D
Unity导入资源提供的选项：automatically calculate normals，不勾选就表示使用自带的顶点法线。

***
`杜郎老矣，想旧事、花须能说。记少年、一梦扬州，二十四桥明月。—周密《瑶华》`