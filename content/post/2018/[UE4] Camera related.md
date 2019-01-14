+++
title= "[UE4]Camera related"
date= "2018-01-12T14:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "PlayerCameraManager"]
+++

keywords: CameraComponent, PlayerController, PlayerCameraManager

##### 设置默认的PlayerCameraManager
PlayerController构造函数中设置PlayerCameraManagerClass：

	PlayerCameraManagerClass = AMyPlayerCameraManager::StaticClass();
	
##### How to Get PlayerCameraManager

	APlayerCameraManager* UGameplayStatics::GetPlayerCameraManager(const UObject* WorldContextObject, int32 PlayerIndex)

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

##### Custom CameraComponent and Default Camera in PlayerCameraManager

There does not have to be a CameraComponent anywhere by default.  
The PlayerController creates a PlayerCameraManager which is all that is needed.  
However, most projects want control over camera parameters and that is done via a CameraComponent.  
The PlayerCameraManager's default parameters are overridden by a CameraComponent via the [documented responsibility chain](https://docs.unrealengine.com/latest/INT/Programming/Gameplay/Framework/Camera/index.html). In the samples, e.g. "Top Down", the CameraComponent can be found inside the character's Blueprint under the Components tab, possibly nested under a SpringArmComponent.


##### Get Camera Location and Rotation

PlayerCameraManager.h

	/**
	 * Master function to retrieve Camera's actual view point.
	 * Consider calling PlayerController::GetPlayerViewPoint() instead.
	 *
	 * @param	OutCamLoc	Returned camera location
	 * @param	OutCamRot	Returned camera rotation
	 */
	void GetCameraViewPoint(FVector& OutCamLoc, FRotator& OutCamRot) const;
	
	/** @return Returns camera's current rotation. */
	UFUNCTION(BlueprintCallable, Category = "Camera")
	FRotator GetCameraRotation() const;

	/** @return Returns camera's current location. */
	UFUNCTION(BlueprintCallable, Category = "Camera")
	FVector GetCameraLocation() const;

##### Reference

Where is the default camera component?  
https://answers.unrealengine.com/questions/26286/where-is-the-default-camera-component.html

Player-Controlled Cameras  
https://docs.unrealengine.com/en-US/Programming/Tutorials/PlayerCamera

Game-Controlled Cameras  
https://docs.unrealengine.com/en-US/Programming/Tutorials/AutoCamera

	
***
`养老江湖外，藏名诗画中。----白狼`