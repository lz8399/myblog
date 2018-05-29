+++
title= "[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与复用)"
date= "2018-05-29T12:36:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Animation"]
keywords= ["UE4", "Animation"]
+++

keyworks：Animation Blueprint Inherit、Animation Blueprint Reuse、蓝图继承、蓝图重用、蓝图复用

三种方式可以重用动画蓝图逻辑：

+ Blueprint Inherit（蓝图继承）
+ Sub Animation Blueprint Instances
+ Post Process Animation Blueprints

##### Animation Blueprint Inherit（动画蓝图继承）
角色蓝图继承和动画蓝图继承有部分相似，这里先说下角色蓝图继承

右键角色蓝图 -》 Create Child Blueprint Class
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-01.jpg">}}

这样创建出来的子蓝图，其构造函数中会自动生成一个执行父级蓝图构造函数的节点
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-02.jpg">}}

其他的Event事件中，如果也需要调用父级蓝图的函数，可以右键对应节点 -》 Add call to parent function
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-03.jpg">}}

{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-04.jpg">}}

动画蓝图也可以使用上述角色蓝图继承的方式。

{{< hl-text red >}}
但直接右键生成子蓝图的方式创建出来的动画蓝图，无法选择其他骨骼，只能保持和父级动画蓝图的骨骼一样
{{< /hl-text >}}

{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-05.jpg">}}

如果要创建一个与父级动画蓝图骨骼不同的子动画蓝图，可以先新建一个普通的动画蓝图
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-06.jpg">}}

然后选择需要继承的父级动画蓝图，以及子动画蓝图的骨骼
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-07.jpg">}}

这样生成出来的子动画蓝图，其Event Graph中，会自动生成一个执行调用父级蓝图的节点：Parent: Blueprint Update Animation
{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-08.jpg">}}

##### Sub Animation Blueprint Instance

{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-09.jpg">}}

Using Sub Anim Instances  
https://docs.unrealengine.com/en-us/Engine/Animation/AnimHowTo/SubAnimInstance

##### Post Process Animation Blueprint

{{< figure src="/img/20180529-[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承与重用)/[UE4][Animation]Animation Blueprint Inherit(动画蓝图继承)-10.jpg">}}
Post Process Anim Blueprint  
https://docs.unrealengine.com/latest/INT/Engine/Animation/Persona/MeshDetails/index.html#skeletalmesh

##### 相关参考
[UE4]How to share character’s blueprint and animation blueprint  
http://smilemugi.net/wordpress/archives/354

Animation Blueprints  
https://docs.unrealengine.com/en-us/Engine/Animation/AnimBlueprints

***
`你以为我贫穷、相貌平平就没有感情吗？我向你发誓，如果上帝赋予我财富和美貌，我会让你无法离开我，就像我现在无法离开你一样。虽然上帝没有这么做，可我们在精神上依然是平等的。---《简爱》`