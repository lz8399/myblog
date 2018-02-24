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

### 异步加载

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

### 同步加载

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

### 资源内存释放
用上述方式加载资源后（包括同步加载和异步加载），如何再释放资源并从内存中销毁？两种情况：

##### 自动回收
`只要对象失去引用后就会被自动释放，无需手动Destroy。如果是异步加载，对象只在回调函数中有效，回调函数执行完毕后，就会被标记为可收回状态，如果此时ForceGC，则对象会立即销毁。`

##### 手动回收
在执行加载时，将bManageActiveHandle标记为true，默认为false：表示是否手动管理FStreamableHandle。如果设置为true，则对象会一直常驻内存直到手动释放。

    FStreamableManager& AssetLoader = UAssetManager::GetStreamableManager();
    UParticleSystem* AimObj = AssetLoader.LoadSynchronous<UParticleSystem>(FSoftObjectPath(AssetPath), true);
    
当对象不再需要时，再手动执行执行Unload。之后对象就会被自动回收：

    FStreamableManager& AssetLoader = UAssetManager::GetStreamableManager();
	AssetLoader.Unload(FSoftObjectPath(AssetPath));

Unload之后如果需要立即回收，可以执行ForceGC：

    GEngine->ForceGarbageCollection(true);

{{< alert danger >}}
在编辑器模式下，上述两种回收方式都不起效，会一直常驻内存，只有在打包运行版本中才会生效。如果在编辑器运行模式下强制Destroy()或者MarkPendingKill()，则对象可以从内存中销毁，但是无法再次Load，除非重启编辑器。
{{< /alert >}}

##### 注意事项
+ FStreamableManager::Unload()会Release掉和当前资源相关的所有FStreamableHandle。比如在三处位置加载了同一个资源，即使bManageActiveHandle设置为true，那么只要调用Unload一次，就可以将这三个FStreamableHandle对象全部Release掉，即从内存中释放该对象；如果对这3个FStreamableHandle对象分别执行Release，那么只有当最后一个Handle被Release之后，该资源才会从内存中释放。

+ 异步加载时，谁先请求则谁的回调函数先执行，不会存在回调函数执行顺序乱序的问题（除非修改TAsyncLoadPriority），因为引擎内部接收回调请求的容器使用的是TArray，且每次执行索引为0的回调，然后RemoveAt(0)。

+ 异步加载时，如果资源还没加载完成就执行ReleaseHandle()（假设加载时bManageActiveHandle为true），比如在执行回调函数之前执行ReleaseHandle，那么当资源加载完成后（回调函数执行之后），会自动从内存中回收。不过该对象在回调函数中仍然有效，除非在回调函数内ForceGC。

        void AMyPlayerController::TestAsyncLoadAndRelease()
        {
            FStreamableDelegate Call;
            Call.BindUFunction(this, FName("AsyncLoadCallback"));
            
            FStreamableManager& AssetLoader = UAssetManager::GetStreamableManager();
            Handle = AssetLoader.RequestAsyncLoad(FSoftObjectPath(AssetPath), Call, 0, true);
            Handle->ReleaseHandle();
        }

##### 参考
《Fortnite》开发经验分享之运行时资源管理：Runtime Asset Management  
https://answers.unrealengine.com/storage/temp/136465-runtimeassetmanagementin416.pdf
