---
title: "[UE4]UObject ConditionalBeginDestroy()导致无法第二次重新Load的问题"
date: "2016-05-28T16:43:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Error
---

如果一个材质对象首次执行垃圾回收（ConditionalBeginDestroy是对BeginDestroy的封装，BeginDestroy是不管任何因素强制回收）：

    UObject::ConditionalBeginDestroy()
或者：

    UObject::BeginDestroy()

之后又需要再次加载该材质，那么调用LoadObject<T>()时，第一个参数不能为NULL:

    UObject* Obj = LoadObject<UObject>(NULL, Path);


因为这样只是在内存中扫描，不会从工程的资源Package文件中去加载(为什么首次这样执行可以加载成功？因为启动UE4Editor或程序首次启动时会自动加载一次)，所以这样不会加载成功，返回值为NULL。
如果要从工程资源文件中加载，那么需要手动new一个UObject，作为LoadObject的第一个参数：

    UObject* Obj = NewObject<UTexture2D>();
    LoadObject<UObject>(Obj, Path);

这样就能正确加载了。
但是这样有个问题：会发现，过几秒以后，再次使用这个UObject时会出现指针非法的错误，原因是刚刚自己New的UObject被引擎从内存中回收了。
如果禁止引擎对该UObject自动垃圾回收，而是我们自己手动执行？执行下AddToRoot：

    Obj->AddToRoot();

注：如果一个UObject是SpawnActor创建出来的，那么执行Destroy()之后，再次执行Spawn是可以正常创建出来的。这点和LoadObject有区别。
