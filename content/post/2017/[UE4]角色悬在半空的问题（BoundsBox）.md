+++
title= "[UE4]角色悬在半空的问题（BoundsBox）"
date= "2017-12-16T13:56:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "BoundsBox"]
+++

可能是场景的StaticMesh的Bounds Box范围有问题，需要在Max或者Maya中修改Bounds Box

{{< figure src="/img/20171216-[UE4]角色悬在半空的问题（BoundsBox）/[UE4]角色悬在半空的问题（BoundsBox）-01.jpg">}}

也可以在UE4中修改Bounds大小
{{< figure src="/img/20171216-[UE4]角色悬在半空的问题（BoundsBox）/[UE4]角色悬在半空的问题（BoundsBox）-02.jpg">}}

{{< alert danger >}}
如果 Static Mesh 用于制作 Destructible Mesh，修改 Static Mesh 的 Bounds 后需要重新创建 Destructible Mesh，否则 Destructible Mesh Bounds还是使用之前的Bounds。另外 Static Mesh 的 Bounds 需要在建模软件中（Max、Maya等）修改，在UE4中修改的Bounds，对 Destructible Mesh 无效。4.20版本是这样，不知道算不算bug。
{{< /alert >}}

***
`衡量一个人的成功标志，不是看他登到顶峰的高度，而是看他跌到低谷的反弹力。----王石`