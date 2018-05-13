+++
title= "[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝"
date= "2017-12-02T21:52:40+08:00"
categories= ["Map-Baking"]
tags= ["Map-Baking", "Maya", "SubstancePainter", "Textures"]
keywords= ["Substance Painter", "Normals Maps Baking", "UV seams", "Cage", "烘焙法线贴图", "接缝"]
+++

Keywords：Substance Painter、Normals Maps Baking、UV seams、Cage、烘焙法线贴图、接缝

这里SP版本为2017.3；Maya版本为2018.1。

#### 1，准备好高模、低模、Cage
这里以Maya为例。  
高模
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-01.jpg">}}

硬边低模
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-02.jpg">}}

低模UV，因为全部是硬边，这里全部切开
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-02-01.jpg">}}

平均法线的Cage
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-03.jpg">}}

##### Cage的制作方式：
这里的Cage是直接在Maya中对硬边低模Duplicate（Ctrl+D）后再扩大（Move Tool），然后再执行平均法线（Mesh Display -》 Average）。  
平均法线之前：
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-04.jpg">}}
平均法线之后：
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-05.jpg">}}

{{< alert danger>}}
注意：是Average Normals平均法线的Cage，不是软边的Cage！否则仍然会有明显的UV接缝。
{{< /alert >}}

平均法线和软边的法线方向还是有略微差距，法线方向如下：  
Cage和低模都为软边
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-06.jpg">}}

Cage为平均法线，低模软边
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-07.jpg">}}

#### 2，将模型的OBJ文件导入SP
先将上述的三个对象导出为OBJ。当前示例导出的3个OBJ文件为：low.obj、high.obj、cage.obj。

然后打开SP，New project（File -》 New）。
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-08.jpg">}}

然后选择前面导出的低模OBJ
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-09.jpg">}}

导入之后，再点击TextureSet Settings面板钟的Bake Textures
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-10.jpg">}}

弹出的Baking面板中，我们只勾选Normal，因为这里只演示法线贴图的烘焙；
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-11.jpg">}}

常用参数解释

+ Output Size：贴图尺寸。
+ High Definition Meshes：高模obj。
+ Use Cage：是否使用cage。
+ Cage File：cage的文件位置。
+ Average Normals：是否使用平均法线。
+ Antialiasing：抗锯齿级别。

烘焙完带cage的法线后，再烘焙一张无cage的法线：去掉勾选Use Cage、Average Normals。
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-12.jpg">}}

将两张法线贴图导出，然后再贴到低模上看效果。（因为在SP上看法线效果区别没有Maya明显，所以这里的的法线预览效果我转到了Maya中查看）  
不同角度上的法线效果如下（为了方便观察，这六张图片未压缩也不加水印）：
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-13.png">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-14.png">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-15.png">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-16.png">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-17.png">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-18.png">}}

#### 扭曲问题
Cage虽然可以更好的处理UV接缝，但是对于凹凸结构会产生扭曲（Distortion），通用的解决方案是在PS中用Cage和无Cage的两张法线贴图合成，将有Cage法线的UV边界合并到无Cage的法线贴图中。篇幅有限这里不讲解如何在PS中合并，后面单独写篇文章讲解如何处理扭曲。
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-19.jpg">}}
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-20.jpg">}}

另外，可以看出：
{{< alert info>}}
如果凹凸结构落差较大，即使是无Cage法线贴图，对于高度的表现并不好，所以对于落差较大的凹凸结构，低模上最好保留相应结构。
{{< /alert >}}

#### 3DMax中的Cage制作(平均法线 Average Normals)

打开菜单：选中 mesh、或patch、或spline、或NURBS object. -》 修改器 > 几何体(转换蒙皮) > 编辑法线。  
Select a mesh, patch, spline, or NURBS object. > Modifiers menu > Geometry (Convert to Mesh) > Edit Normals
{{< figure src="/img/20171202-[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝/[Map-Baking]SP烘焙法线贴图：使用Cage处理UV接缝-21.png">}}

然后点击：“法线” -》 “选择” -》 修改。

官方文档：Edit Normals Modifier Reference  
https://knowledge.autodesk.com/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2016/ENU/3DSMax/files/GUID-82722323-100B-4711-A01D-8A87EB53DD96-htm.html

***
`若无力驾驭，自由便是负担。`