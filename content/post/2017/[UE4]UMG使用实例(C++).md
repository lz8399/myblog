+++
title= "[UE4]UMG使用实例(C++)"
date= "2017-11-08T15:06:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UMG", "C++", "Widget", "Demo", "Example", "示例", "实例", "例子", "UI"]
+++

Keywords：UE4、UMG、C++、Widget、Demo、Example、示例、实例、例子、UI

两年前写过一篇C++操控UMG蓝图的文章，当时写的有点乱，非核心的东西写了不少，干扰阅读（当时自己刚学UE4，完全懵逼）。另外最新版本中，UMG不需要在Build.cs中添加配置，默认即可。  
这里用4.18版本重新做一个C++控制UMG的精简实例，完整工程下载见文章底部。

假设新建的测试工程叫：UMGTest。实现一个简单的功能：点击按钮，动态替换掉按钮上的背景图片。

UMG使用步骤如下：
##### 1，创建自定义的UMG C++类。
在UE4编辑器中点击：File -》 New C++ Class。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-01.jpg">}}

弹出的对话框中，勾选Show All Classes，并找到UserWidget，选中后再点击Next。表示选择UserWidget作为我们创建的C++ class的父类。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-02.jpg">}}

起好名字（这里命名为：MyUserWidget），点击创建
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-03.jpg">}}

##### 2，创建UMG蓝图
在内容浏览器中，右键点击：User Interface  -》 Widget Blueprint。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-04.jpg">}}

修改蓝图名称并保存。这里命名为：NewWidgetBlueprint。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-05.jpg">}}

然后双击打开UMG蓝图，拖拽一个Button组件到编辑视图中。假设给这个Button命名为：BtnChangeImg。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-06.jpg">}}

并设置按钮的大小，这里设置为和图片素材一样的大小
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-07.jpg">}}

再拖拽一个Image组件到这个Button内
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-08.jpg">}}

并设置Image组件的大小
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-09.jpg">}}
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-10.jpg">}}

然后切换到Graph视图
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-11.jpg">}}

然后再点击Class Settings
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-12.jpg">}}

再找到Parent Class，设置为之前创建的C++类：MyUserWidget。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-13.jpg">}}

##### 3，编写自定义UserWidget的C++代码
添加需要的头文件，比如我们在头文件中使用了UImage，那么需要指明这个UImage所在的头文件。例如：

	#include "Components/Image.h"

具体代码如下：

**UMGTestGameModeBase.h**

	// Fill out your copyright notice in the Description page of Project Settings.

	#pragma once

	#include "CoreMinimal.h"
	#include "GameFramework/GameModeBase.h"
	#include "UMGTestGameModeBase.generated.h"

	/**
	 * 
	 */
	UCLASS()
	class UMGTEST_API AUMGTestGameModeBase : public AGameModeBase
	{
		GENERATED_BODY()

	public:

		AUMGTestGameModeBase();

	protected:

		virtual void BeginPlay() override;
		
	private:

		//UMG蓝图的实例对象，用于显示在游戏的Viewport中UUserWidget* MyWidgetInstance;
	};

**UMGTestGameModeBase.cpp**

	// Fill out your copyright notice in the Description page of Project Settings.

	#include "UMGTestGameModeBase.h"
	#include "Blueprint/UserWidget.h"

	AUMGTestGameModeBase::AUMGTestGameModeBase()
	{
		MyWidgetInstance = NULL;
	}

	void AUMGTestGameModeBase::BeginPlay()
	{
		//检测Widget对象是否存在，如果存在则移除掉。
		if (MyWidgetInstance)
		{
			MyWidgetInstance->RemoveFromViewport();
			MyWidgetInstance = nullptr;
		}

		//加载自定义UMG的class，通过这个class创建Widget对象，并显示在界面中。
		if (UClass* MyWidgetClass = LoadClass<UUserWidget>(NULL, TEXT("WidgetBlueprint'/Game/NewWidgetBlueprint.NewWidgetBlueprint_C'")))
		{
			if (APlayerController* PC = GetWorld()->GetFirstPlayerController())
			{
				MyWidgetInstance = CreateWidget<UUserWidget>(PC, MyWidgetClass);
				if (MyWidgetInstance)
				{
					MyWidgetInstance->AddToViewport();
				}
			}
		}
	}

**MyUserWidget.h**

	// Fill out your copyright notice in the Description page of Project Settings.

	#pragma once

	#include "CoreMinimal.h"
	#include "Blueprint/UserWidget.h"
	#include "Components/Image.h"

	#include "MyUserWidget.generated.h"

	/**
	 * 
	 */
	UCLASS()
	class UMGTEST_API UMyUserWidget : public UUserWidget
	{
		GENERATED_BODY()

	public:

		UMyUserWidget(const FObjectInitializer& ObjectInitializer);
		
	protected:

		virtual void NativeConstruct() override;

		UFUNCTION()
			void OnBtnChangeImgClick();

	private:

		//英雄头像的显示图片
		UImage* HeroIcon;

		//两张图片素材
		UTexture2D* TexHero1;
		UTexture2D* TexHero2;

		//显示状态标识
		int ImgFlag;

	};

**MyUserWidget.cpp**

	// Fill out your copyright notice in the Description page of Project Settings.

	#include "MyUserWidget.h"
	#include "Components/Button.h"
	#include "Engine/Texture2D.h"

	UMyUserWidget::UMyUserWidget(const FObjectInitializer& ObjectInitializer) : Super(ObjectInitializer)
	{
		HeroIcon = NULL;
		TexHero1 = NULL;
		TexHero2 = NULL;
		ImgFlag = 0;
	}

	void UMyUserWidget::NativeConstruct()
	{
		Super::NativeConstruct();

		//根据组件ID查找Image组件
		if (UImage* img = Cast<UImage>(GetWidgetFromName(FName(TEXT("ImgHero")))))
		{
			HeroIcon = img;
		}

		//根据组件ID查找Button组件，并为其添加Click回调事件
		if (UButton* btn = Cast<UButton>(GetWidgetFromName("BtnChangeImg")))
		{
			FScriptDelegate Del;
			Del.BindUFunction(this, "OnBtnChangeImgClick");
			btn->OnClicked.Add(Del);
		}

		//加载图片资源
		if (TexHero1)
		{
			//如果已经加载过，则先销毁掉
			TexHero1->ConditionalBeginDestroy();
			TexHero1 = NULL;
			GetWorld()->ForceGarbageCollection(true);
		}
		TexHero1 = LoadObject<UTexture2D>(NULL, TEXT("Texture2D'/Game/pic_01.pic_01'"));

		if (TexHero2)
		{
			TexHero2->ConditionalBeginDestroy();
			TexHero2 = NULL;
			GetWorld()->ForceGarbageCollection(true);
		}
		TexHero2 = LoadObject<UTexture2D>(NULL, TEXT("Texture2D'/Game/pic_02.pic_02'"));
	}

	void UMyUserWidget::OnBtnChangeImgClick()
	{
		//切换显示图片
		if (HeroIcon && TexHero1 && TexHero2)
		{
			HeroIcon->SetBrushFromTexture(ImgFlag ? TexHero1 : TexHero2);
			ImgFlag = ImgFlag == 0 ? 1 : 0;
		}
	}


##### 最终效果
按Shift+F1切换到光标显示模式，然后点击按钮，就可以切换图片。
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-14.jpg">}}
{{< figure src="/img/20171108-[UE4]UMG使用实例(C++)/[UE4]UMG使用实例(C++)-15.jpg">}}

完整工程下载地址：  
http://pan.baidu.com/s/1i5em6TR