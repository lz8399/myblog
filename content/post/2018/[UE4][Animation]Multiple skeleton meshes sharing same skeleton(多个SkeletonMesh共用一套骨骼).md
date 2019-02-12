+++
title= "[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)"
date= "2018-05-29T12:30:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Animation"]
keywords= ["UE4", "Animation", "customizable character","换装"]
+++

keywords：UE4 Animation、Set Master Pose Component、customizable character、动画蓝图、换装

##### 美术资源制作
1. 每个身体部件（帽子、鞋子等）蒙皮时需要使用同一套骨骼(all pieces need to be skinned to the same skeleton)
2. 每个身体部件导出时，该部件的关节与根关节之间的所有关节都需要选中导出。例如：假设盆骨为根关节（root joint），现在要导出手臂，那么手臂、肩膀、脊椎、盆骨的关节都需要选中导出。

##### 角色蓝图中设置Master Pose

身体各个部件导入UE4之后，打开角色蓝图，为每个部件Add一个Skeleton Mesh Component，并将其Skeleton Mesh属性设置为对应的资源文件。

{{< figure src="/img/20180529-[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)/[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)-01.jpg">}}

{{< figure src="/img/20180529-[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)/[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)-02.jpg">}}

{{< figure src="/img/20180529-[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)/[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)-03.jpg">}}

最后在BeginPlay事件中执行`Set Master Pose Component`

{{< figure src="/img/20180529-[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)/[UE4][Animation]Multiple skeleton meshes sharing same skeleton(多个SkeletonMesh共用一套骨骼)-04.jpg">}}

这样，角色在播放动画时，每个部件就会跟随角色一起播放，而不会固定不动。

参考自：How to Setup "Master Pose Component"  
https://answers.unrealengine.com/questions/228601/how-to-setup-master-pose-component.html

{{< alert danger >}}
注意事项：不要在构造函数中执行`SetMasterPoseComponent`，否则会出现莫名其妙的问题，比如：Mesh的LOD失效。
{{< /alert >}}

How to make SetMasterPoseComponent work with skeletal meshes with LODs?  
https://answers.unrealengine.com/questions/793802/how-to-make-setmasterposecomponent-work-with-skele.html



##### C++接口

`Set Master Pose Component`蓝图节点对应的C++ API：

    Child->SetMasterPoseComponent(Body);

***
`有一个传说，说的是有那么一只鸟儿，它一生只唱一次，那歌声比世上所有一切生灵的歌声都更加优美动听。---《荆棘鸟》`