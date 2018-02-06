+++
title= "[UE4]资源异步加载(Assets Asynchronous Loading)与内存释放(Free Memory)"
date= "2018-01-26T00:42:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Asset Asynchronous Loading"]
+++

为什么需要异步加载资源，因为当一次性加载的资源较多或者单个资源较大时，普通的LoadObject()方式会阻塞引擎的主线程。

假设测试工程叫TestTD4，自定义Character叫ATestTD4Character（头文件为TestTD4Character.h）

假设在Content/Assets/目录下放了三个动画文件（AnimSequence）。

##### 通过DefaultGame.ini配置文件生成FSoftObjectPath

DefaultGame.ini

	[/Script/TestTD4.TestTD4Character]
	+TestAssets=/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump
	+TestAssets=/Game/Assets/ThirdPersonRun.ThirdPersonRun
	+TestAssets=/Game/Assets/ThirdPersonWalk.ThirdPersonWalk

TestTD4Character.h

	UPROPERTY(Config)
			TArray<FSoftObjectPath> TestAssets;

这个属性的意思是：加Config标签表示从DefaultGame.ini读取，TestAssets就是DefaultGame.ini中配置的属性名，当游戏启动时，这个数组会被自动填充3个元素，即资源的路径。

{{< alert warning>}}
注：4.18版本中FStringAssetReference、TAssetPtr两个变量被重命名为：FSoftObjectPath、TSoftObjectPtr.
{{< /alert >}}


TestTD4Character.cpp

	void ATestTD4Character::BeginPlay()
	{
		Super::BeginPlay();

		for (FSoftObjectPath& Asset : TestAssets)
		{
			GEngine->AddOnScreenDebugMessage(-1, 3, FColor::Cyan, Asset.ToString());
		}

		FStreamableManager& AssetLoader = UAssetManager::GetStreamableManager();
		AssetLoader.RequestAsyncLoad(TestAssets, FStreamableDelegate::CreateUObject(this, &ATestTD4Character::AnimAssetsDeferred));
	}

	void ATestTD4Character::AnimAssetsDeferred()
	{
		for (FSoftObjectPath SoftObj : TestAssets)
		{
			TAssetPtr<UAnimSequence> AnimAsset(SoftObj);

			UAnimSequence* AnimObj = AnimAsset.Get();
			if (AnimObj)
			{
				GEngine->AddOnScreenDebugMessage(-1, 3, FColor::Red, AnimObj->GetName());
			}
		}
	}

	
打印结果：

	ThirdPersonWalk
	ThirdPersonRun
	ThirdPerson_Jump
	/Game/Assets/ThirdPersonWalk.ThirdPersonWalk
	/Game/Assets/ThirdPersonRun.ThirdPersonRun
	/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump

如果注掉RequestAsyncLoad，直接执行AnimAssetsDeferred()，则打印结果为：

	/Game/Assets/ThirdPersonWalk.ThirdPersonWalk
	/Game/Assets/ThirdPersonRun.ThirdPersonRun
	/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump

说明这三个资源确实是运行时异步加载，而不是游戏启动时就被自动加载。

##### 通过路径字符串生成FSoftObjectPath

头文件中定义一个变量

	FSoftObjectPath SoftObj;

在cpp函数中通过路径赋值（比如在BeginPlay()函数中）

	SoftObj = FSoftObjectPath(TEXT("/Game/Mannequin/Animations/ThirdPersonWalk.ThirdPersonWalk"));
	FStreamableManager& AssetLoader = UAssetManager::GetStreamableManager();
	AssetLoader.RequestAsyncLoad(SoftObj, FStreamableDelegate::CreateUObject(this, &AUMGTestGameModeBase::AnimAssetsDeferred));

回调函数中获取对象

	void ATestTD4Character::AssetsDeferred()
	{
		TAssetPtr<UAnimSequence> WidgetAsset(SoftObj);
		UAnimSequence* AnimObj= WidgetAsset.Get();
		if (AnimObj)
		{
			GEngine->AddOnScreenDebugMessage(-1, 3, FColor::Red, AnimObj->GetName());
		}
	}

{{< alert danger>}}
注意：UserWidget蓝图无法通过上述方式执行异步加载，目前只测试了Animation、Mesh等资源是可行的。
{{< /alert >}}

##### 同步加载

同步加载有两种API：

+ FStreamableManager::LoadSynchronous

		UAnimSequence* AimObj = AssetLoader.LoadSynchronous<UAnimSequence>(FSoftObjectPath(TEXT("/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump")));

+ FStreamableManager::RequestSyncLoad

		TSharedPtr<FStreamableHandle> Handle = AssetLoader.RequestSyncLoad(FSoftObjectPath(TEXT("/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump")));
		if (Handle.IsValid())
		{
			UAnimSequence* AnimiObj = Cast<UAnimSequence>(Handle->GetLoadedAsset());
		}

{{< alert warning>}}
FStreamableManager的源码注释已经写明：RequestAsyncLoad、RequestSyncLoad、LoadSynchronous等待延迟时间可能长达数秒。LoadSynchronous和RequestSyncLoad的内部实现是对异步加载的封装：调用FStreamableHandle::WaitUntilComplete()阻塞等待。RequestSyncLoad函数内部要么会进行异步载入并且调用WaitUntilComplete函数，要么直接调用LoadObject函数 —— 哪个更快就调哪个。
{{< /alert >}}

##### 资源内存释放
用上述方式加载资源后（包括同步加载和异步加载），如何再释放资源并从内存中销毁？  
方式如下：

	FSoftObjectPath Path(TEXT("/Game/Assets/ThirdPerson_Jump.ThirdPerson_Jump"));
	AssetLoader.Unload(Path);
	Path.ResolveObject()->MarkPendingKill();
	GEngine->ForceGarbageCollection();

{{< alert danger>}}
FStreamableManager加载出来的资源不会被垃圾回收，会常驻内存，只有执行Unload()并且MarkPendingKill()后，才会从内存销毁。但是从内存销毁后，无法再用FStreamableManager Load资源，会返回NULL。
{{< /alert >}}

Runtime Asset Management  
https://answers.unrealengine.com/storage/temp/136465-runtimeassetmanagementin416.pdf