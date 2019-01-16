+++
title= "[UE4]3 ways of adding OnClicked Event for Actor(both CPP and Blueprint)"
date= "2018-01-11T23:30:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Character", "OnClick", "C++", "Blueprint"]
+++

keywords：如何获取鼠标点击时的物体对象、鼠标悬停事件、鼠标点击事件、鼠标单击事件

# Mouse Clicked Event

### Method 1: GetHitResult

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

### Methd 2: Override NotifyActorOnClicked()

	void AActor::NotifyActorOnClicked(FKey ButtonPressed = EKeys::LeftMouseButton) override;
	
Steps:

1. Set `bEnableClickEvents` to true.
	
		APlayerController::bEnableClickEvents = true;
	
2. Override function `NotifyActorOnClicked`

		void AMyActor::NotifyActorOnClicked(FKey ButtonPressed)
		{
			Super::NotifyActorOnClicked(ButtonPressed);
			GEngine->AddOnScreenDebugMessage(-1, 1.f, FColor::Red, FString("++++++++++"));
		}
	
3. {{< hl-text red >}}If use Character to reveive Clicked Event, Capsule's "CollisionProfile" must be set as "BlockAllDynamic", default is "Pawn".{{< /hl-text >}}

		GetCapsuleComponent()->SetCollisionProfileName("BlockAllDynamic");
		
If want to use Character's default CollisionProfile "Pawn" to receive Clicked Event, `Visibility` must to be set as `Block`( Project Settings -> Engine -> Collision -> Preset -> Pawn -> Trace Type -> Visibility).
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-11.jpg">}}
		
### Methd 3: Use OnClicked Delegate

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

选中 Capsule 后，再在Detail面板中点击OnClick事件
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-05.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-06.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-07.jpg">}}


### How to use Character's default CollisionProfile and Trace Type to receive Clicked Event

If you don't want to change Character's default CollisionProfile (`Pawn`) and don't want to change Trace Type of CollisionProfile `Pawn`, you can add a BoxComponent or a Cube StaticMeshComponent on Character to receive Clicked Event.

{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-01.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-02.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-03.jpg">}}
{{< figure src="/img/20180111-[UE4]Character添加OnClick事件（C++和蓝图两种方式）/[UE4]Character添加OnClick事件（C++和蓝图两种方式）-04.jpg">}}
	

##### Reference

OnClicked not working in C++(works in bp)  
https://answers.unrealengine.com/questions/389222/mouse-click-not-working-in-cworks-in-bp.html

# Mouse Over Event

Steps:

1. Override function:

		virtual void AActor::NotifyActorBeginCursorOver() override;

		virtual void AActor::NotifyActorEndCursorOver() override;

2. Set `bEnableMouseOverEvents` to true.
 
		APlayerController::bEnableMouseOverEvents = true;

***
`盖天地之道，日中必移，月满必亏，泽满则溢。----《易经》`