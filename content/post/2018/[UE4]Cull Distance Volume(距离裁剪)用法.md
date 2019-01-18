+++
title= "[UE4]Cull Distance Volume(距离裁剪)用法"
date= "2018-03-04T13:42:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Cull Distance Volume"]
+++

keywords：UE4、Cull Distance Volume、距离裁剪、遮挡剔除


##### 排除物体
打开编辑器，在World Outline（不是Content Browser中的static mesh双击后的编辑面板，而是static mesh拖拽到场景中之后的实例对象的属性面板）。选中要排除的物体，打开Show All Advanced Details，找到LOD -》 去掉勾选 All Cull Distance Volume。
{{< figure src="/img/20180304-[UE4]Cull Distance Volume(遮挡剔除)用法/[UE4]Cull Distance Volume(遮挡剔除)用法-01.jpg">}}

##### 常用的Distance级别设置
{{< figure src="/img/20180304-[UE4]Cull Distance Volume(遮挡剔除)用法/[UE4]Cull Distance Volume(遮挡剔除)用法-02.jpg">}}

##### 遮挡剔除没有效果的原因

可能有3中原因：

1. `Enabled`没有勾选；
2. 体积设置的太小，物体不在`Cull Distance Volume`范围内；
3. {{< hl-text red >}} 引擎的bug（切换引擎版本后导致。如果升级引擎版本，建议重新建一个空白场景），Cull Distance Volume在游戏运行时才有效，在编辑器非运行期间拖拉摄像机无效。 {{< /hl-text >}}


***
`识不足则多虑；威不足则多怒；信不足则多言。----弘一法师`