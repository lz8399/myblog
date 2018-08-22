+++
title= "[UE4] Camera 摄像机相关"
date= "2018-01-12T14:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "PlayerCameraManager"]
+++

##### 设置默认的PlayerCameraManager
PlayerController构造函数中设置PlayerCameraManagerClass：

	PlayerCameraManagerClass = AMyPlayerCameraManager::StaticClass();

##### 摄像机不跟随角色一起旋转

	USpringArmComponent::bAbsoluteRotation = true;
    
##### 摄像机视角范围限定

默认情况下，执行 `APlayerController->AddPitchInput()` 上下旋转摄像机视角时，会有范围限制：最上不能超过90度，最下不能超过-90度。  
这个范围限定是`PlayerCameraManager`的属性控制的，视角范围限定的六个属性：

    /** Minimum view pitch, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewPitchMin;

	/** Maximum view pitch, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewPitchMax;

	/** Minimum view yaw, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewYawMin;

	/** Maximum view yaw, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewYawMax;

	/** Minimum view roll, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewRollMin;

	/** Maximum view roll, in degrees. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=PlayerCameraManager)
	float ViewRollMax;

	
***
`养老江湖外，藏名诗画中。----白狼`