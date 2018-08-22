+++
title= "[UE4]Character添加OnClicked事件（C++和蓝图两种方式）"
date= "2018-01-11T23:30:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Character", "OnClick", "C++", "Blueprint"]
+++

keywords：如何获取鼠标点击时的物体对象

### 方式一：添加Cube（Static Mesh Component）

{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-01.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-02.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-03.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-04.jpg">}}

##### C++方式

MyCharacter.cpp构造函数中注册回调：

	OnClicked.AddUniqueDynamic(this, &ATestTD2Character::OnSelected);

回调函数：

MyCharacter.h

	UFUNCTION()
		void OnSelected(AActor* Target, FKey ButtonPressed);

MyCharacter.cpp

	void MyCharacter::OnSelected(AActor* Target, FKey ButtonPressed)
	{
		GEngine->AddOnScreenDebugMessage(-1, 2.f, FColor::Cyan, FString("EEEEEEEEEEEEEEEEE"));
	}

##### 蓝图方式

选中Cube后，再在Detail面板中点击OnClick事件
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-05.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-06.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-07.jpg">}}


### 方式二：GetHitResult

1，Project Settings中编辑Input配置
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-08.jpg">}}


如果要用鼠标模式触屏输入方式，如要勾选Use Mouse for Touch。

2，C++中注册回调：先给PlayerController注册Input事件

	void AMyPlayerController::SetupInputComponent()
	{
		//鼠标点击
		InputComponent->BindAction("MouseClick", IE_Pressed, this, &AMyPlayerController::OnMouseClick);

		//触屏输入 support touch devices 
		InputComponent->BindTouch(EInputEvent::IE_Pressed, this, &AMyPlayerController::OnFingerTouch);
	}

	void AMyPlayerController::OnMouseClick()
	{
		FHitResult HitResult;
		GetHitResultUnderCursor(ECollisionChannel::ECC_Pawn, false, HitResult);

		if (HitResult.GetComponent())
		{
			GEngine->AddOnScreenDebugMessage(-1, 2, FColor::Red, FString::Printf(TEXT("Mouse Click+++ Component: %s"), *HitResult.GetComponent()->GetName()) );
		}

		if (HitResult.GetActor())
		{
			GEngine->AddOnScreenDebugMessage(-1, 2, FColor::Red, FString::Printf(TEXT("Mouse Click+++ Actor: %s"), *HitResult.GetActor()->GetName()));
		}
	}

	void AMyPlayerController::OnFingerTouch(const ETouchIndex::Type FingerIndex, const FVector Location)
	{
		FHitResult HitResult;
		GetHitResultUnderFinger(ETouchIndex::Type::Touch1, ECollisionChannel::ECC_Pawn, false, HitResult);

		if (HitResult.GetComponent())
		{
			GEngine->AddOnScreenDebugMessage(-1, 2, FColor::Red, FString::Printf(TEXT("Finger Touch +++ Component: %s"), *HitResult.GetComponent()->GetName()));
		}

		if (HitResult.GetActor())
		{
			GEngine->AddOnScreenDebugMessage(-1, 2, FColor::Red, FString::Printf(TEXT("Finger Touch +++ Actor: %s"), *HitResult.GetActor()->GetName()));
		}
	}

##### 点击角色后的效果

鼠标点击输入
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-09.jpg">}}

触屏输入
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-10.jpg">}}


##### 参考
OnClicked not working in C++(works in bp)  
https://answers.unrealengine.com/questions/389222/mouse-click-not-working-in-cworks-in-bp.html

***
`盖天地之道，日中必移，月满必亏，泽满则溢。----《易经》`