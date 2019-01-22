+++
title= "[UE4]性能优化指南(美术向)"
date= "2018-11-22T12:13:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Performance", "Optimization"]
+++

参考自官方文档：  
Performance Guidelines for Artists and Designers  
<!--more-->
https://docs.unrealengine.com/en-us/Engine/Performance/Guidelines

但是官方文档写的太粗燥，对UE4没有一定了解，很难理解文档的意图。这里我在官方文档的基础上，结合自己遇到的问题，重新整理了一下，适合对UE4不熟的美术查阅。

以下是针对美术人员和关卡设计师的常规提升性能的指导意见

##### 面向美术

+ 尽量减少每个物体上的元件数量。比如概设美术在设计角色形象时，有没必要为了表现效果为角色加很多装饰性部件，要把握好。如果是做静帧动画没什么问题，但若是实时渲染的游戏角色，要做取舍。
+ 为了让元件的三角面数更合理（比如每个元件的面数为300+），建议相关模型合并起来。比如，如果游戏没有换装需求，那么就将角色的帽子、肩甲等身体部件和身体合并，以减少面数。
+ Opaque贴图（不透明贴图）速度最快，因为它的Z buffer裁切速度最快；Masked贴图（蒙版贴图）稍微慢一点；Translucent贴图（半透明贴图）最慢，因为其性能消耗巨大。
+ 限制UV接缝数量和硬边（Maya中叫软硬边、Max和Blender中叫光滑组）数量，因为这两项会在硬件中生成大量顶点。最坏的情况，带硬边的高模会生成3倍于建模软件统计的顶点数（比如：Maya中显示模型顶点数为1万，显卡中实际计算的顶点数为3万）。
+ Skined Mesh（蒙皮网格物体）的顶点处理性能消耗比Static Mesh（静态网格物体）的高。比如，一个建筑从地面升起的动画，这种只是整个模型坐标的变化，就不要让动作美术去K动画，而应该使用UE4的Timeline去控制StaticMesh的坐标变化，以提升性能；再比如门打开关闭的动画，也不要去手K，可以参考官方ContentExamples中的使用Timeline的做法。
+ 当使用了morph targets（比如表情动画）或者WorldPositionOffset（世界坐标偏移），顶点处理的消耗会大大增加。因为要做缓存，贴图的查找过程也会非常慢。
UE4材质中的Morph Targets：
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-01.jpg">}}
UE4材质中的WorldPositionOffset：
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-02.jpg">}}
+ Tessellation（曲面细分）的性能消耗巨大（UE4提供了的运行时曲面细分），尽量避免使用；Pre-tessellation（预处理曲面细分，就是手动在建模软件中做好细分曲面）通常速度更快。（现在的次世代流程大部分都是使用法线贴图+低模，也有部分次世代游戏在使用曲面细分，比如PS4游戏《地平线：黎明时分》）
UE4材质中的Tessellation Multiplier（开启方式：修改`D3D11Tessellation Mode`）：
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-03.jpg">}}
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-04.jpg">}}
Maya中制作细分曲面流程  
https://www.youtube.com/watch?v=L5fOwSmSaW8
+ 非常大的物体建议拆成多块，这样可以更好的做视距裁切和灯光裁切
+ 贴图格式越小则材质性能越好。比如：DXT1格式为4 bpp（每像素的比特位数），DXT5格式为8 bpp，未压缩的ARGB为32 bpp。
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-05.jpg">}}
{{< alert warning >}}对于有Alpha通道的贴图，默认的DXT1格式会压缩过度，不支持Alpha通道，导致效果丢失，此时可以修改为低压缩率的格式，比如：UserInterface2D(RGBA){{< /alert >}}
+ 贴图尺寸越小性能越好（当贴图近距离显示时）。有时更小的贴图尺寸甚至更加平滑，作为双线性过滤（bilinear filtering ）时，比贴图格式能提供更多的着色器（shader）效果。
+ 材质减少着色器指令（shader instruction）和贴图数量，运行时的查找过程更快。为了优化材质，可以使用UE4材质编辑器中的stats统计（材质编辑器顶部菜单）以及材质复杂度（ShaderComplexity，运行模式下F5，场景编辑模式下Alt + 8，绿色表示消耗极低，白色表示消耗极高）。  
点击Stats，查看贴图采样数、贴图查找时长等。
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-06.jpg">}}
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-07.jpg">}}
点击Platform Stats，查看各个平台的性能统计（桌面级、安卓、iOS等）
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-08.jpg">}}
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-09.jpg">}}
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-10.jpg">}}
+ 如果贴图在很小的范围内还能看见（比如视线远处的模型LOD），则不要禁用纹理贴图（Mip Maps），否则会由于贴图缓存缺失而导致性能下降。  
Mip Gen Settings 设置为 NoMipmaps表示禁用。
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-11.jpg">}}
+ 一些材质蓝图的计算表达式比较耗，比如：sin、pow、cos、divide、Noise；消耗较低的计算表达式包括：multiply、add、subtract、clamp。
+ 阴影模型（shading models，最常见的光照模型，游戏工业中用得多）的性能消耗标准：无光的区域消耗最低，有光的区域是消耗较大，这也是最常见的区域。其他光照模型（比如照明模型Illumination models，电影工业的光照模型）的性能消耗更大。

#### 面向关卡设计

+ 限制Stationary（固定光源，不是静态光源）和 Dynamic（动态光源） 灯光的数量。
+ 尽量避免使用区域光源（Area light）。4.20提供了区域光源 Rect Light。
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-12.jpg">}}
+ 对场景中较小的物体，编辑其属性draw distance来获得更佳的LOD裁切效果
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-13.jpg">}}
确保LOD设置在一个激进变化的范围内（比如摄像机从很近一下拉倒很远，距离变化很小的不用做LOD），写LOD的定点数量变化倍数至少是两倍。优化时，打开wireframe模式，然后查看是否存在大的色块，如果有说明优化有问题。如果使用Simplygon（一款商业付费的UE4插件），几分钟就可以处理掉整个项目的LOD。
+ 尽量将类似信息的光源合并。比如，车的头灯可以用一个光源以及一个光照函数让它看起来是两个灯的效果。
+ 静态光照最快，固定光照稍慢一些，动态光照最慢。
+ 按照需要，尽量限制光照的衰减半径以及光锥的角度。
+ 动态/固定点光源是最费的。方向光源要稍好一些，最好的是聚光灯光源。阴影贴图生成的性能开销和造成物体阴影的光照视锥体（light frustum）有关。
+ 光照函数具有额外的性能开销（实际开销取决于材质），并能防止灯光被渲染成 Tiled Light。
+ IES profiles 具有额外性能开销（比光照函数好一些），并能防止灯光被渲染成 Tiled Light。但不要在可以用聚光灯光锥就能完成效果的情形下，还使用 IES。
+ Billboards，imposter meshes，或 skybox textures 都能用来代替实际的几何体物件并有效的提高性能。
+ 好的关卡设计师能够将遮蔽裁剪纳入考虑优化关卡（添加一些阻挡视线的物件来提高性能）。使用 r.VisualizeOccludedPrimitives 可以直接查看。  
控制台命令开启遮挡物件可视化:
	
		r.VisualizeOccludedPrimitives 1
	
{{< figure src="/img/20181122-[UE4]性能优化指南(美术向)/[UE4]性能优化指南(美术向)-14.jpg">}}

+ 避免使用 Light Propagation Volumes，如果要使用，使用 GIReplace 材质表达式，或者在大部分物件上禁用它，以提升性能。
+ 在不需要的地方应该关闭阴影生成（ shadow cast），一个个物件的关闭，或者一个个灯光来关闭。
+ 在编辑器中使用 ProfileGPU（Ctrl + Shift + ,）快速了解信息以及哪部分比较慢。
+ 贴花的性能开销和它们覆盖的像素数量有关。



***
`必然的王国必然地过去了，自由的王国自由得不肯来，现在是什么王国呢？这个查之有头，望不见尾的“现在”。──木心《真的》`
