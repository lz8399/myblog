---
title: "[UE4]注意事项与笔记"
date: "2015-12-06T22:50:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

1，如何添加自己的C++代码

如果是添加Character C++代码，是在UE4 Editor中添加的，但是如果想添加一些与UE4引擎无关的c++代码，比如网络通讯的，或者一些工具类，必须也在UE4 Editor中添加（至少我现在用的4.10版本是这样），如果在VS中直接添加，会出现一些奇怪的编译错误。UE4 Editor中添加自定义C++代码方式如下：
File -> New C++ Class -> 选择None，然后即可创建自己C++代码

2，UE4还写莫名其妙的bug，这些bug可能是与操作系统有关，建议用Windows7，解决办法：重新建个空的工程，然后把你现在项目的资源文件重新加进去，然后在编译和构建。

我的windows10上遇到了果断奇怪问题有：

(1)，项目自定义的GameMode没生效，进游戏是默认的自由摄像机控制器。这个问题我没有重新建工程，而是把level删掉重新建了一次。

(2)，打包安卓Android部署时，提示错误：DistributionSigning settings are not all set. Check the DistributionSetting

3，[2016-05-15]如果项目中使用了LoadClass<T>，那么蓝图相关的class构造函数中不要执行和实例化对象相关的操作，因为当执行LoadClass时也会把对应class的构造函数执行一遍（即使我们没有手动执行spawn或者create等函数，原因是LoadClass执行了LoadObject，而LoadObject内部又会执行ConstructorHelpers::FObjectFinder()，所以会触发class的构造函数，比如自己新建了一个UserWidget class，这个class的默认构造函数会在LoadClass时被执行一次），建议将初始化操作放在Initialize、BeginPlay等函数中。

4，[2015-05-17]内存溢出导致的问题：在用FString拼接字符串的时候，抛了一个异常，但是相同的代码在另一个地方是正常的，两个地方都是非GameThread，崩掉的位置发在调用FString::FromInt()。后来用itoa代替就正常了。很可能是逻辑代码有内存溢出的bug。

5，[2016-06-02]如果同一属性在蓝图编辑器中和C++中的值不同，那么蓝图中的属性值会shadow掉C++构造函数中的值。如果想让C++的值shadow蓝图的值，那么可以在C++的BeginPlay等非构造函数的初始化函数中设置属性（这里假设没有在蓝图逻辑脚本中对属性设置）。
新建蓝图时，蓝图的属性会遵循C++父类中的构造函数中的属性设置。

6，[2016-08-16]用C++动态创建Component时，在`AttachToComponent`之前，需要执行`RegisterComponent`,否则无法Attach成功。备注：这个问题貌似要看版本，新版本中貌似不需要执行`RegisterComponent`，具体我没实测过。

7，[2016-09-23]UE4中的C++类继承规则：只能直接继承自两种类，一种是非UObject类，一种是继承过UInterface的UObject类。如果一个类是UObject且其父类没有一个是UInterface，则无法编译通过。

8，如果同一批美术材质，在两个不同工程下的渲染效果不一样，比如同一个粒子特效，实际效果在两个工程中有差异，则可能是工程的设置项问题。解决办法：将两个工程中的Config/DefaultEngine.ini中的[/Script/Engine.RendererSettings]配置参数，设置统一即可。

9，如果spawn出来的actor执行了AddToRoot操作，那么，需要GameInstance::Shutdown()中执行RemoveFromRoot，否则退出UE4Editor时会出现崩溃。另外，在GameMode和GameInstance的BeginDestroy()中执行是不行的，因为垃圾回收过程发生在BeginDestroy()执行之前。