---
title: "[UE4]UObject ConditionalBeginDestroy相关"
date: "2016-05-28T16:43:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Error
---

##### UObject ConditionalBeginDestroy()导致无法第二次重新Load的问题

现象：  
如果一个材质对象首次执行垃圾回收（ConditionalBeginDestroy是对BeginDestroy的封装，BeginDestroy是不管任何因素强制回收）：

    UObject::ConditionalBeginDestroy()
或者：

    UObject::BeginDestroy()

之后又需要再次加载该材质，那么调用LoadObject<T>()时，第一个参数不能为NULL:

    UObject* Obj = LoadObject<UObject>(NULL, Path);

原因：  
在编辑器模式下，通过`LoadObject`加载出来的对象，如果执行了Destroy，那么在不重启编辑器模式的情况下，第二次执行`LoadObject<UObject>(NULL, Path);`会返回`NULL`，即使在编辑器模式下重新启动游戏也返回`NULL`

解决办法：  
上述情况只存在编辑器模式下，如果是打包版本，即使一开始 Destroy，第二次 LoadObject 的时候仍然可以加载成功。  

如果非得希望在编辑器模式下，Destroy资源之后仍然能够正常第二次 LoadObject 该资源，方式如下：  
{{< hl-text green>}}手动new一个UObject，作为LoadObject的第一个参数{{< /hl-text >}}

    UObject* Obj = NewObject<UTexture2D>();
    LoadObject<UObject>(Obj, Path);

这样就能正确加载了。

通过上述表现可以推算出，编辑器和引擎的Runtime公用了同一个对象

+ 且该对象没有随着编辑器模式下退出游戏而被清理；
+ 且该对象在编辑器和Runtime分别存在一个是否已销毁的标记；
+ 且该对象在PIE（Play In Editor）模式下 Destroy 后，并没有标记该对象在编辑器中已非法；

所以在PIE模式下第二次 LoadObject 时认为该对象还存在，并且直接返回了这个已经被Destroy的空对象。  
如果UE4资源管理的引擎代码写的足够好，对于Destroy对象的操作，应该提供两个版本：一个PIE、一个Game Runtime。

##### 内存持久化 (Memory Persistence)

上述问题中，即使在第二次加载时手动 NewObject 创建一个对象，仍然存在问题：会发现，过几秒以后，再次使用这个UObject时会出现指针非法的错误，原因是刚刚自己New的UObject被引擎从内存中回收了。
如何禁止引擎对该UObject自动垃圾回收，而是我们自己手动执行？执行下AddToRoot：

    Obj->AddToRoot();

注：如果执行了`AddToRoot()`，那么退出程序前需要执行`RemoveFromRoot()`，否则在引擎在清理内存时会错误。

{{< hl-text red>}}如果一个UObject是SpawnActor创建出来的，那么执行Destroy()之后，再次执行Spawn是可以正常创建出来的。这点和LoadObject有区别。{{< /hl-text >}}

##### ConditionalBeginDestroy()并不推荐在业务逻辑中使用

{{< alert warning >}}
UE4官方论坛上，很多帖子或资料告诉你，如果要销毁对象，需要执行ConditionalBeginDestroy()。其实这个API不是给上层逻辑使用的，如果要销毁对象，只要保证该对象失去引用或者RemoveFromRoot()即可，否则就会出现上述问题，即：Destroy之后，无法第二次Load。但是这个问题只存在编辑器运行模式下，如果是打包版本（或者Play时选择下拉菜单：Standalone），即使Destroy()，第二次LoadObject()，第一个参数为NULL，也是可以正常加载的。
{{< /alert >}}

##### DedicatedServer 中的问题
{{< alert danger >}}
如果在 DedicatedServer 模式下，SpawnActor生成Actor，且这个Actor bReplicates 设置为true，执行 ConditionalBeginDestroy() ，一定时间后客户端会崩掉，但是使用 Destroy() 没问题。对于服务端生成的 Actor，销毁对象时绝对不要 ConditionalBeginDestroy()。
{{< /alert >}}

解决办法：  
`SpawnActor`生成出的 Actor，且 `AActor::bReplicates = true;` ，销毁时，不要用`ConditionalBeginDestroy()`，而要用`Destroy()`。Standalone 模式貌似没这种限制。

崩溃日志：
	
	Assertion failed: Index >= 0 [File:D:\Build\++UE4+Release-4.16+Compile\Sync\Engine\Source\Runtime\CoreUObject\Public\UObject/UObjectArray.h] [Line: 455] 

	UE4Editor_Core!FDebug::AssertFailed() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\private\misc\assertionmacros.cpp:349]
	UE4Editor_Engine!UNetDriver::ServerReplicateActors_BuildConsiderList() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:2600]
	UE4Editor_Engine!UNetDriver::ServerReplicateActors() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:3159]
	UE4Editor_Engine!UNetDriver::TickFlush() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\networkdriver.cpp:355]
	UE4Editor_Engine!TBaseUObjectMethodDelegateInstance<0,UNetDriver,void __cdecl(float)>::ExecuteIfSafe() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\public\delegates\delegateinstancesimpl.h:858]
	UE4Editor_Engine!TBaseMulticastDelegate<void,float>::Broadcast() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\core\public\delegates\delegatesignatureimpl.inl:937]
	UE4Editor_Engine!UWorld::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\engine\private\leveltick.cpp:1506]
	UE4Editor_UnrealEd!UEditorEngine::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\editor\unrealed\private\editorengine.cpp:1633]
	UE4Editor_UnrealEd!UUnrealEdEngine::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\editor\unrealed\private\unrealedengine.cpp:386]
	UE4Editor!FEngineLoop::Tick() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\launchengineloop.cpp:3119]
	UE4Editor!GuardedMain() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\launch.cpp:166]
	UE4Editor!GuardedMainWrapper() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:134]
	UE4Editor!WinMain() [d:\build\++ue4+release-4.16+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:210]
	UE4Editor!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:253]
	kernel32
	ntdll

##### ConditionalBeginDestroy 和 Destroy区别
ConditionalBeginDestroy 和 Destroy两者都是销毁对象，区别是：前者是在delay一定时间后执行销毁，Destroy是在当前帧结束时执行销毁。

如果逻辑上每帧都有很多 Actor需要销毁，那么可以先把这些Actor隐藏，让对象失去引用（如果对象是被`URPOPERTY`属性保持的，那就让其所属的对象失去引用，比如：`RemoveFromRoot()`），不必手动执行 Destroy，让引擎批量执行GC。
