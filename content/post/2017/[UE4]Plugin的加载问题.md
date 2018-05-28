+++
title= "[UE4]How to Install a Plugin on Unreal Engine"
date= "2017-12-17T00:56:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Plugin"]
+++

在GameMode构造函数中加载（LoadObject或者ConstructorHelpers::FObjectFinder）蓝图，该蓝图使用了plugin（这里我使用了一个叫Swipe的插件），如果在构造函数中加载，则会报错：

	/Game/Demo/Female/Blueprints/FemaleCharBP : Can't find file for asset. /Script/Swipe
	Failed to load /Script/Swipe.SwipeComponent Referenced by K2Node_ComponentBoundEvent_2
	Failed to load /Script/Swipe.SwipeComponent Referenced by K2Node_ComponentBoundEvent_3
	Failed to load /Script/Swipe.SwipeComponent Referenced by SCS_Node_1

解决办法：成员变量（LoadObject返回值，在构造函数中创建的对象）添加UPROPERTY()宏。

另外一种解决办法：给C++的GameMode套一个蓝图，然后在该蓝图中设置DefaultPawnClass、PlayerControllerClass等GameMode属性，此时即使这些PawnClass或者PlayerControllerClass蓝图使用了plugin，也不会报错。

***
`醉里挑灯看剑，梦回吹角连营。----辛弃疾《破阵子·为陈同甫赋壮词以寄之》`