---
title: "[UE4]注意事项与笔记"
date: "2015-12-06T22:50:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

我的老博客中的UE4文章  
http://aigo.iteye.com/category/347833

【2015-12-06】  
如何添加自己的C++代码  
如果是添加Character C++代码，是在UE4 Editor中添加的，但是如果想添加一些与UE4引擎无关的c++代码，比如网络通讯的，或者一些工具类，必须也在UE4 Editor中添加（至少我现在用的4.10版本是这样），如果在VS中直接添加，会出现一些奇怪的编译错误。UE4 Editor中添加自定义C++代码方式如下：
File -> New C++ Class -> 选择None，然后即可创建自己C++代码

UE4还写莫名其妙的bug，这些bug可能是与引擎升级有关，可参考解决办法：重新建个空的工程，然后把你现在项目的资源文件重新加进去，然后在编译和构建。

我的windows10上遇到的奇怪问题有：  

(1)，项目自定义的GameMode没生效，进游戏是默认的自由摄像机控制器。这个问题我没有重新建工程，而是把level删掉重新建了一次。

(2)，打包安卓Android部署时，提示错误：DistributionSigning settings are not all set. Check the DistributionSetting

【2016-05-15】  
如果项目中使用了LoadClass<T>，那么蓝图相关的class构造函数中不要执行和实例化对象相关的操作，因为当执行LoadClass时也会把对应class的构造函数执行一遍（即使我们没有手动执行spawn或者create等函数，原因是LoadClass执行了LoadObject，而LoadObject内部又会执行ConstructorHelpers::FObjectFinder()，所以会触发class的构造函数，比如自己新建了一个UserWidget class，这个class的默认构造函数会在LoadClass时被执行一次），建议将初始化操作放在Initialize、BeginPlay等函数中。

【2015-05-17】  
内存溢出导致的问题：在用FString拼接字符串的时候，抛了一个异常，但是相同的代码在另一个地方是正常的，两个地方都是非GameThread，崩掉的位置发在调用FString::FromInt()。后来用itoa代替就正常了。很可能是逻辑代码有内存溢出的bug。

【2016-06-02】  
如果同一属性在蓝图编辑器中和C++中的值不同，那么蓝图中的属性值会shadow掉C++构造函数中的值。如果想让C++的值shadow蓝图的值，那么可以在C++的BeginPlay等非构造函数的初始化函数中设置属性（这里假设没有在蓝图逻辑脚本中对属性设置）。
新建蓝图时，蓝图的属性会遵循C++父类中的构造函数中的属性设置。

【2016-08-16】  
用C++动态创建Component时，在`AttachToComponent`之前，需要执行`RegisterComponent`,否则无法Attach成功。备注：这个问题貌似要看版本，新版本中貌似不需要执行`RegisterComponent`，具体我没实测过。

【2016-09-23】  
UE4中的C++类继承规则：只能直接继承自两种类，一种是非UObject类，一种是继承过UInterface的UObject类。如果一个类是UObject且其父类没有一个是UInterface，则无法编译通过。

如果同一批美术材质，在两个不同工程下的渲染效果不一样，比如同一个粒子特效，实际效果在两个工程中有差异，则可能是工程的设置项问题。解决办法：将两个工程中的Config/DefaultEngine.ini中的[/Script/Engine.RendererSettings】配置参数，设置统一即可。

如果spawn出来的actor执行了AddToRoot操作，那么，需要GameInstance::Shutdown()中执行RemoveFromRoot，否则退出UE4Editor时会出现崩溃。另外，在GameMode和GameInstance的BeginDestroy()中执行是不行的，因为垃圾回收过程发生在BeginDestroy()执行之前。

【2017-02-06】  
用宏控制debug相关代码的开启和关闭

    #if UE_BUILD_SHIPPING
        //debug code...
    #endif
 

UE4数据同步相关的引擎源码  

    Runtime\Engine\Private\ActorReplication.cpp
    Runtime\Engine\Private\ Replication.cpp
    Runtime\Engine\Public\Net \DataReplication.cpp
    Engine\Plugins\Messaging\TcpMessaging\Source\TcpMessaging\Private\TcpMessagingModule.cpp

 

FActorSpawnParameters意义  
SpawnActor()有个参数：FActorSpawnParameters，这个参数中有很多属性，设置相关属性后，可以更方便的来控制这个被spawn出来的Actor，比如Owner属性：

    FActorSpawnParameters Param;
    Param.Owner = MyActor1;  
    AActor MyActor2 = GetWorld()->SpawnActor<MyActor>(MyClass, Param);
    //此时的Owner就是MyActor1
    MyActor Owner= MyActor2->GetOwner();



获取当前角色视角的起始location和rotation  
APawn::GetActorEyesViewPoint();


获取模型缸体尺寸的相关API  
AActor::GetSimpleCollisionXXXX()
比如：AActor::GetSimpleCollisionHalfHeight()、AActor::GetSimpleCollisionRadius()

 

【2017-02-08 21:00】  
AActot::FinishSpawning()的作用  
一个Actor被Spawn出来之后，再调用FinishSpawning，会触发OnConstruct()、PostInitializeComponents()、BeginPlay()等函数。


Rotation、Vector转换为Matrix的API  
FRotationMatrix(const FRotator& Rot)，其父类为FRotationTranslationMatrix(const FRotator& Rot, const FVector& Origin);    

 

【2017-02-14 15:06】  
UE4Editor命令行执行GM命令的方式  
在非shipping模式下，按下波浪键，输入：AdminCheat PlayerController中的函数名 参数1 参数2 …… 。  
比如：AdminCheat TestFun 11 abc  
敲回车后，就会去执行自定义PlayerController中的TestFun函数，参数的两个参数值为11、abc。


【2017-02-20】  
AActor::OwnedComponents  
OwnedComponents是当前Actor所拥有的所有Components。

UWorld::TimeSince(double time)  
返回time与当前系统时间的时间差。

AActor::GetWorldTimerManager().SetTimerForNextTick()  
设置下一个tick期间执行的回调函数。

AActor::ForceNetUpdate()  
强制将当前actor的数据更新到客户端。

UPritimiComponent::MoveIngoreActors  
如果希望当前actor移动或者触发Overlap事件时，忽略掉和某些Component之前的物理计算，则可以将这些Component加入MoveIngoreActors。

UPrimitiveComponent作用  
注释中的解释是：PrimitiveComponent通常包括：ShapeComponents，StaticMeshComponent，SkeletalMeshComponent。


【2017-02-23】  
FRotator::RotateVector(const FVector& V) 与 FMatrix::TransformVector()区别  
两者都是用来对方向向量进行转向计算的，FRotator::RotateVector()只是对FMatrix::TransformVector进行了封装，FMatrix::TransformVector是一般数学函数库都提供的函数，FRotator::RotateVector()是UE4放了方便作Vector转向计算，将FVector转换为FMatrix的操作封装在RotateVector()函数内部。  
Unity3D提供的类似封装为：function TransformDirection (direction : Vector3) : Vector3


CharacterMovementComponent一些重要接口：IsWalkable()、PhysWalking()、PhysFlying()、PhysCustom()

 

 

【2017-02-28】  

设置Character的自定义MovemenComponentt或者CapsuleComponent  
在构造函数中设置：  

旧版本方式

    MyCharacter:: MyCharacter(const FPostConstructInitializeProperties& PCIP) : Super(PCIP.SetDefaultSubobjectClass<MyCharacterMovement>(ACharacter::CharacterMovementComponent))
    {
    }

 

新版本方式（FPostConstructInitializeProperties换成FObjectInitializer）

    MyCharacter:: MyCharacter(const FObjectInitializer& ObjectInitializer) : Super(ObjectInitializer.SetDefaultSubobjectClass<MyCharacterMovement>(ACharacter::CharacterMovementComponent))
    {
    }



TArray的排序用法
如果有一组Character对象，想以他们的坐标和某个特定坐标作比较并排序，方式如下：

    TArray<ACharacter > Arr;
    FVector FromLoc(1000.f, 1000.f, 0.f);
    Arr.Sort(FactorArrayDistanceSort2D(FromLoc));


UE4编译蓝图的引擎API  
FKismetCompilerModule::CompileBlueprint()，其内部回去创建一个FBlueprintCompileReinstancer对象，该对象内部会创建待编译蓝图的DuplicatedClass。
ULinkerLoad::CreateExport(int index)，其内部会去加载蓝图引用的相关资源。


【2017-03-20】  
Reference Viewer中的资源引用关系  
如果箭头从左到右，则表示左边的资源有引用右边的资源。比如，左边资源的某个属性是右边的资源，或者左边的父类是右边的资源。


RenderUtils.h  
该Util类中的一些纯色的全局贴图对象，可以直接调用，比如：GWhiteTexture。



【2017-06-03】  
4.16 bug，资源无法cook，在编辑器中运行正常，但是打包时无法cook资源。建议先不要用4.16，目前4.16.1版本仍然没有修复该问题。
网上有种说法，说把模型动作全部通过fbx重新导入一遍，不要直接使用旧的*.uasset，但是我试了下仍然无法解决。

【2017-06-12】  
蓝图属性无法访问的问题  
蓝图A中的属性或者函数，在蓝图B中，无法通过蓝图A的实例来访问。  
原因是这些属性和函数设置为了private。

【2017-06-14】  
FVector::GetMin()和FVector::GetMax()，两个API的作用分别是获取x、y、z三个数中的最小/最大值

【2017-06-17】  
安装VS2017时，需要勾选Windows SDK 8.1，如果只勾选最新的SDK 10，则UE4工程无法生成VS工程文件。

【2017-11-09】
Instanced Static Mesh  
Instancing是UE4批量渲染提供的一种性能优化机制，比如一片森林，一种只有3种形态的树木（Mesh），但每种树木在场景中会出现200棵。
unity5.4也提供了类似的功能：Instancing。

相关资料：  
Instanced Static Mesh Decreasing performance!  
https://forums.unrealengine.com/development-discussion/blueprint-visual-scripting/40156-instanced-static-mesh-decreasing-performance/page2

UE4 Optimization: Instancing  
https://www.youtube.com/watch?v=oMIbV2rQO4k

Instanced Static Mesh  
https://docs.unrealengine.com/latest/INT/BlueprintAPI/Components/InstancedStaticMesh/

Blueprint Generating Procedural Rooms | Live Training | Unreal Engine  
https://www.youtube.com/watch?v=mI7eYXMJ5eI

【2017-11-18T23:10】
如何导入Maya、3D Max、Blender动画的Blend Shape(Morph Targets)

FBX Morph Target Pipeline
https://docs.unrealengine.com/latest/INT/Engine/Content/FBX/MorphTargets/

Morph Target Previewer  
https://docs-origin.unrealengine.com/latest/INT/Engine/Animation/Persona/MorphTargetPreviewer/
