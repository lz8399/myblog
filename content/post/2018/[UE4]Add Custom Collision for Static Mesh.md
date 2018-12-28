+++
title= "[UE4]Add Custom Collision for Static Mesh"
date= "2018-09-27T16:57:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

对于结构简单的模型，使用UE4自动生成的Simple Collision没什么问题；如果模型结构复杂，使用Simple Collision不够精准，使用Complex Collision对于实时计算（比如开放世界大场景的游戏项目）的项目来说太耗。

##### UE4中自定义碰撞盒

Static Mesh默认打开后：
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-01.jpg">}}

勾选 Simple Collision
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-02.jpg">}}

然后选中 Collision，按Delete键删掉
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-03.jpg">}}

然后点击菜单 Collision -》 Add Box Simplified Collision
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-04.jpg">}}

然后就可以按W、E、R键修改 Box的坐标、转向、缩放等
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-05.jpg">}}
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-06.jpg">}}
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-07.jpg">}}

由于缩放比例是按倍数调整的，所以一个box很难完整包裹物体，这个时候可以使用多个Box组合，例如：
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-08.jpg">}}


官方文档：  
Setting Up Collisions With Static Meshes  
https://docs.unrealengine.com/en-us/Engine/Content/Types/StaticMeshes/HowTo/SettingCollision

##### 在3DMax、Maya中创建自定义碰撞盒

UE4编辑器中虽然提供了添加自定义碰撞盒的功能，但是编辑起来不够灵活，对于特殊形状的物体，建议在建模软件中创建自定义碰撞盒。

1，比如U型物体，UE4自动生成的碰撞盒子是这样的：  
简单碰撞
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-09.jpg">}}

复杂碰撞
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-10.jpg">}}

2，我们在建模软件中（这里以Maya为例），为U型物体添加三块遮挡方块
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-11.jpg">}}

将U型物体和3个方块合成一个Group，{{< hl-text red >}}并且碰撞盒子的命名一定要遵循规则：UCX_主物体名XXX。例如：主物体名称为pCylinder，则碰撞盒子的名称必须为：UCX_pCylinderXXX，否则导入UE4后这3个方块会被当作真实物体而不是碰撞体。{{< /hl-text >}}
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-12.jpg">}}

然后导出FBX文件，导入UE4时，去掉勾选：Auto Generate Collision；如果碰撞盒子没有和模型合成一个Group，还需要勾选：Combine Meshes。这里我们已经在Maya进行了Group操作，所以可以不用勾选 Combine Meshes。
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-13.jpg">}}

导入UE4后，编辑器中打开该物体，然后勾选：Collision -》 Simple Collision
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-14.jpg">}}

就可以看到3块自定义碰撞盒。
{{< figure src="/img/20181109-[UE4]Add Custom Collision for Static Mesh/[UE4]Add Custom Collision for Static Mesh-15.jpg">}}
