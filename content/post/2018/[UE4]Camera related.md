+++
title= "[UE4]Camera related"
date= "2018-01-12T14:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "PlayerCameraManager"]
+++

keywords: CameraComponent, PlayerController, PlayerCameraManager

##### Set default PlayerCameraManager

Set PlayerCameraManagerClass in constructor of PlayerController:

	PlayerCameraManagerClass = AMyPlayerCameraManager::StaticClass();
	
##### How to Get PlayerCameraManager

	APlayerCameraManager* UGameplayStatics::GetPlayerCameraManager(const UObject* WorldContextObject, int32 PlayerIndex)

##### Enable camera rorate by controller, not keep the same rotation of character

CPP

	USpringArmComponent::bAbsoluteRotation = true;
	
Blueprint

{{< figure src="/img/20180112-[UE4]Camera related/[UE4]Camera related-01.jpg">}}
    
##### Limit rotate range of camera

When execute `APlayerController->AddPitchInput()`, Camera would look up in limited range by default: from -90 degrees down to 90 degrees up.  
This limited range is affected by properties of `PlayerCameraManager`, there're 6 properties to limit the range of camera rotation:

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
	
##### How to set offset of SpringArm and CameraComponent

Set `SocketOffset` or `TargetOffset`, `SocketOffset` is at end of spring arm, `TargetOffset` is at start of spring. 

	/** offset at end of spring arm; use this instead of the relative offset of the attached component to ensure the line trace works as desired */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Camera)
	FVector SocketOffset;

	/** Offset at start of spring, applied in world space. Use this if you want a world-space offset from the parent component instead of the usual relative-space offset. */
	UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Camera)
	FVector TargetOffset; 
	
{{< alert danger >}}
If want to relative location of CameraComponent, don't use SetRelativeLocation or AddRelativeLocation on SpringArmComponent, otherwise there is jolt on camera where character moving.
{{< /alert >}}
	
	
##### How to disable collision detect of SpringArm

Set `bDoCollisionTest` to false,

	USpringArmComponent::bDoCollisionTest = false;
	
##### How to disable WASD for camera movement

Set `bAddDefaultMovementBindings` to false in the constructor, default value is true.

Reference  
https://answers.unrealengine.com/questions/193289/is-there-a-way-to-disable-wasd-for-camera-movement.html

##### Reference

Where is the default camera component?  
https://answers.unrealengine.com/questions/26286/where-is-the-default-camera-component.html

Player-Controlled Cameras  
https://docs.unrealengine.com/en-US/Programming/Tutorials/PlayerCamera

Game-Controlled Cameras  
https://docs.unrealengine.com/en-US/Programming/Tutorials/AutoCamera

	
***
`养老江湖外，藏名诗画中。----白狼`