+++
title= "[UE4]Plugin相关"
date= "2017-12-17T00:56:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Plugin"]
+++

##### Plugin在构造函数中加载的问题

在GameMode构造函数中加载（LoadObject或者ConstructorHelpers::FObjectFinder）蓝图，该蓝图使用了plugin（这里我使用了一个叫Swipe的插件），如果在构造函数中加载，则会报错：

	/Game/Demo/Female/Blueprints/FemaleCharBP : Can't find file for asset. /Script/Swipe
	Failed to load /Script/Swipe.SwipeComponent Referenced by K2Node_ComponentBoundEvent_2
	Failed to load /Script/Swipe.SwipeComponent Referenced by K2Node_ComponentBoundEvent_3
	Failed to load /Script/Swipe.SwipeComponent Referenced by SCS_Node_1

另外一种解决办法：给C++的GameMode套一个蓝图，然后在该蓝图中设置DefaultPawnClass、PlayerControllerClass等GameMode属性，此时即使这些PawnClass或者PlayerControllerClass蓝图使用了plugin，也不会报错。

###### 添加第三方Plugin（2018-08-10更新）

工程.uproject 需要添加两处地方：  
1，在 Modules 中添加 plugin 名字字符串；  
2，在 Plugins 添加 plugin 信息：包括 Name 和 Enabled；

    {
      "FileVersion": 3,
      "EngineAssociation": "4.20",
      "Category": "",
      "Description": "",
      "Modules": [
        {
          "Name": "TowerDefense",
          "Type": "Runtime",
          "LoadingPhase": "Default",
          "AdditionalDependencies": [
            "UMG",
            "Engine",
            "CoreUObject",
            "AIModule",
            "ApexDestruction",
            "RTSAI"
          ]
        }
      ],
      "Plugins": [
        {
          "Name": "ApexDestruction",
          "Enabled": true
        },
        {
          "Name": "RTSAI",
          "Enabled": true
        }
      ]
    }

##### 参考资料

How to Install a Plugin on Unreal Engine 4  
https://idkudk.blogspot.jp/2015/02/how-to-install-plugin-on-unreal-engine-4.html

UE4/Plugin installation  
https://wiki.popcornfx.com/index.php/UE4/Plugin_installation

***
`醉里挑灯看剑，梦回吹角连营。----辛弃疾《破阵子·为陈同甫赋壮词以寄之》`