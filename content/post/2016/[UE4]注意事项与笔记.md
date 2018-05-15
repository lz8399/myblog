---
title: "[UE4]注意事项与笔记"
date: "2015-12-06T22:50:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

我的老博客中的UE4文章（一百八十多篇，未迁移，和此博客的UE4文章不重叠）  
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

【2016-05-17】  
内存溢出导致的问题：在用FString拼接字符串的时候，抛了一个异常，但是相同的代码在另一个地方是正常的，两个地方都是非GameThread，崩掉的位置发在调用FString::FromInt()。后来用itoa代替就正常了。很可能是逻辑代码有内存溢出的bug。

【2016-06-02】  
如果同一属性在蓝图编辑器中和C++中的值不同，那么蓝图中的属性值会shadow掉C++构造函数中的值。如果想让C++的值shadow蓝图的值，那么可以在C++的BeginPlay等非构造函数的初始化函数中设置属性（这里假设没有在蓝图逻辑脚本中对属性设置）。
新建蓝图时，蓝图的属性会遵循C++父类中的构造函数中的属性设置。

【2016-08-16】  
用C++动态创建Component时（NewObject<Component>()），在`AttachToComponent`之前，需要执行`RegisterComponent`,否则无法Attach成功。备注：只有NewObject创建出来的Component才需要执行ResisterComponent，SpawnActor和ConstructorHelpers创建的对象则不需要。

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


获取模型刚体尺寸的相关API  
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
强制并立即将当前actor的数据更新到客户端。

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

【2017-12-07T19:01】  
4.18的Build.cs编译错误：  
error : g:\Source\Work\Game20171205\program\client\TestTD\Source\TestTD\TestTD.Build.cs(31,9) : error CS0246: 未能找到类型或命名空间名称“FileReference”(是否缺少 using 指令或程序集引用?)

解决办法：  
在Build.cs中添加命令空间：  
using Tools.DotNETCommon;

【2017-12-07T19:45】  
UE4集成Protobuf 3.5版本时的一些问题  
错误：wire_format_lite.h(863): error C4146: unary minus operator applied to unsigned type, result still unsigned  
解决办法：disable warning或者切换到3.4版本

错误：type_traits(605): error C4647: behavior change: __is_pod(google::protobuf::internal::AuxillaryParseTableField) has different value in previous versions  
解决办法：  
修改generated_messages_table_driven.h  
将  
static_assert(std::is_pod<AuxillaryParseTableField>::value, "");  
注释掉

UE4集成3.X版本的protobuf有一些问题（比如无法静态链接protobuf-lite.lib），建议能用2.x版本就用2.x版本。

相关参考：  
https://github.com/hanbim520/protobuffer-for-Unreal-Engine-4-/issues/1  
https://medium.com/@0xflarion/using-ue4-w-google-protocol-buffers-ae7cab820d84

【2017-12-08T18:57】  
BUILD FAILED：gradle\rungradle.bat" :app:assembleDebug

4.18安卓项目发送到手机上的时候出现错误代码 ExceptionUtils.PrintExceptionInfo: ERROR: cmd.exe failed with args /c "D:\Stage - kornelis\ARcore\HelloARSample 4.18\Intermediate/Android/APK\gradle\rungradle.bat" :app:assembleDebug ExceptionUtils.PrintExceptionInfo: 

解决方案：  
1，双击NVPACK/android-sdk-windows/tools/android.bat  
2，点击"Deselect All"，取消所有选中  
3，勾选：Extras/Android Support Repository，然后点击Install。  

【2017-12-10T18:57】 
UObject::ConditionalBeginDestroy()是异步销毁对象内存；AActor::Destroy();是同步销毁对象内存且是在当前帧结束时立即执行。这里说的销毁不是硬指针delete内存，而是从内存池中抹掉数据。

【2017-12-14T14:24】  
编译时引擎代码报错：

	'SetPipelineState': illegal qualified name in member declaration

解决办法：  
修改 engine\source\runtime\d3d12rhi\private\D3D12StateCachePrivate.h(716) 

将  
D3D12_STATE_CACHE_INLINE void FD3D12StateCacheBase::SetPipelineState(FD3D12PipelineState* PSO)
修改为  
D3D12_STATE_CACHE_INLINE void SetPipelineState(FD3D12PipelineState* PSO)

参考：  
https://answers.unrealengine.com/questions/605554/setpipelinestate-illegal-qualified-name-in-member.html

【2017-12-21T16:27】  
1，GameMode无法在游戏运行过程中切换，只能在编辑器的WorldSettings或者Project Settings中切换。

2，How can I get the current map name? 获取当前地图的名称。

	GetWorld()->GetMapName();

但是这种方式获取的名字有引擎自动添加的前缀，比如在内容浏览器中场景名为test_scene，用此API获取的名字为xxx_test_scene。

3，UEngine::Browse和UEngine::LoadMap都是用于客户端本地加载场景，区别是：前者是对后者的封装：包括判断当前WorldContext是否有挂起未完成的LoadMap请求。

【2017-12-25T14:31】  
角色蓝图的摄像机无法编辑的问题  
问题现象：在角色蓝图中，如果选中摄像机组件后，Detail面板中为空，相关参数看不见，可能该角色蓝图是在纯蓝图项目创建的，此时再指定其父类为C++ Character class，则会出现这种情况：即父类C++中暴露的Camera属性在蓝图中不可编辑。  
解决办法：重新建一个空白角色蓝图，然后再指定其父类C++ class，然后再编辑。

【2017-12-26T15:04】  
问题现象：在GameMode::BeginPlay()函数中，SpawnActor多个角色，但是有的角色没有显示，但是隐藏的角色能用TObjectIterator遍历出来。  
可能原因：SpawnActor时的Z坐标太低，穿插了地面。  
解决办法：SpawnActor时Z坐标调高。  

【2017-12-27T16:21】  
如何限定UPROPERTY值的范围(Range)

	///Specifies the lowest that the value slider should represent.
	UIMin

	///Specifies the highest that the value slider should represent.
	UIMax

	///Specifies the minimum value that may be entered for the property.
	ClampMin

	///Specifies the maximum value that may be entered for the property.
	ClampMax
 
示例

	UPROPERTY(EditAnywhere, Category = "Test", meta=(ClampMin = "0.0", ClampMax = "300.0", UIMin = "0.0", UIMax = "300.0"))

【2017-12-27T17:31】  
如何修改角色的移动速度

	if (UCharacterMovementComponent* Movement = MyCharacter->GetCharacterMovement())
	{
		Movement->MaxWalkSpeed *= 0.5;
	}

【2017-12-28T13:57】  
如果UMG中的一个button，在游戏运行时，鼠标一放上去鼠标光标就消失，原因是button的`IsFocusable`属性设置为false。

【2018-01-12T19:09】  
MoveToLocation和AddMovementInput同时执行  
如果对同一个Pawn，同时使用AIController::MoveToLocation()和APawn::AddMovementInput()来移动物体，会有冲突，会出现短暂时间内角色被黏住无法移动的情况

【2018-01-03T10:26】  

	void AActor::AttachToComponent(USceneComponent* Parent, const FAttachmentTransformRules& AttachmentRules, FName SocketName)

AttachToComponent()的参数SocketName，也可以是骨骼名，即使不添加Socket，也可以直接用骨骼来挂载物件。

【2018-01-04T16:56】  
如何在TMap中存放一个TArray数组

	USTRUCT()
	struct FConversations
	{
		UPROPERTY()
		TArray<FString> Entries;
	};

	TMap<EConversationNode, FConversations> testMap;

Is there any way to store an array in a tmap?  
https://answers.unrealengine.com/questions/319040/is-there-any-way-to-store-an-array-in-a-tmap.html?sort=oldest

【2018-01-08T16:56】  
如何在运行时期间隐藏显示虚拟摇杆（Virtual Joystick）

	void APlayerController::SetVirtualJoystickVisibility(bool bVisible);


【2018-01-13T14:08】  
Switch Level时能保留的数据  
Switch Level时能保留的数据对象只有一个：GameInstance。GameState、PlayerState都会被重置。


【2018-02-05T16:01】  
SceneComponent和ActorComponent的区别  
SceneComponent有transform属性（location, rotation, scale）而ActorComponent没有。  
意义在于：如果只是存放数据，而不处理显示逻辑，那么就用ActorComponent，如果需要处理显示上的层级关系（比CameraComponent机与SpringArm），那么要用SceneComponent。

【2018-02-09T10:30】  
Android打包时的OpenGL和Vulkan支持  
Project Settings -》 Platforms -》 Android -》 Build -》 Support OpenGL ES3.1。默认只使用OpenGL ES2。

【2018-03-01T12:28】  
使用 Skeletal Control 动态控制头部IK运动  
http://blog.csdn.net/sb978433018/article/details/77429762

【2018-03-21T11:48】  
DerivedDataCache目录修改  
默认目录在
C:\Users\用户名\AppData\Local\UnrealEngine\Common\DerivedDataCache，时间久了以后，该目录的体积会有十几个G。  
修改方法：打开UE4Editor -》 Edit -》 Editor Preference -》General -》 Global -》 Derived Data，修改位置。

【2018-03-22T14:42】  
游戏暂停时是否允许输入执行（默认是禁止输入）

    FInputActionBinding& ToggleInGameMenuBinding = InputComponent->BindAction("InGameMenu", IE_Pressed, this, &AStrategyPlayerController::OnToggleInGameMenu);
    ToggleInGameMenuBinding.bExecuteWhenPaused = true;

【2018-03-26T14:42】  
错误：

    FAsyncPackage::FindExistingImport class mismatch int property 
    
原因：在UObject构造函数中去执行了BindUFunction()等逻辑。  
解决办法：在非构造函数中执行，比如BeginPlay()或者NativeContruct()（UserWidget而言）。

【2018-05-03T15:32】  
隐藏安卓的虚拟键、软键 Hide Android App Soft Keys(Home key and Return key)  
Project Settings -》 Android -》 Platforms -》 Enable FullScreen Immersive on KitKat and above devices

【2018-0515T20:17】  
UMG BindWidget宏使用  
假如在UMG蓝图中放了一个name为BtnTest的UButton，那么可以在父类C++的UserWidget类中使用meta = (BindWidget)，来获取这个button的指针：

    UPROPERTY(meta = (BindWidget))
		UButton* BtnTest;

这样就不用通过GetWidgetFromName()函数获取button的指针：

    BtnTest = Cast<UButton>(GetWidgetFromName(TEXT("BtnTest")));

***
`凡心所向，素履以往。生如逆旅，一苇以航。----木心`