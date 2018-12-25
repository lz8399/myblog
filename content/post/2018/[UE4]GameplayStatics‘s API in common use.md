+++
title= "[UE4]GameplayStatics‘s API in common use"
date= "2018-11-22T15:08:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UGameplayStatics", "GameplayStatics"]
+++

keywords: UGameplayStatics, GameplayStatics

{{< alert danger >}}
Parameter `WorldContextObject` must be an UObject that can get UWorld, otherwise the following gameplay's functions would not work.
{{< /alert >}}

    /**
	* Counts how many grass foliage instances overlap a given sphere.
	*
	* @param	Mesh			The static mesh we are interested in counting.
	* @param	CenterPosition	The center position of the sphere.
	* @param	Radius			The radius of the sphere.
	*
	* @return Number of foliage instances with their mesh set to Mesh that overlap the sphere.
	*/
	UFUNCTION(BlueprintCallable, Category = "Foliage", meta = (WorldContext = "WorldContextObject", UnsafeDuringActorConstruction = "true"))
	static int32 GrassOverlappingSphereCount(const UObject* WorldContextObject, const UStaticMesh* StaticMesh, FVector CenterPosition, float Radius);

	/** 
	 * Transforms the given 2D screen space coordinate into a 3D world-space point and direction.
	 * @param Player			Deproject using this player's view.
	 * @param ScreenPosition	2D screen space to deproject.
	 * @param WorldPosition		(out) Corresponding 3D position in world space.
	 * @param WorldDirection	(out) World space direction vector away from the camera at the given 2d point.
	 */
	UFUNCTION(BlueprintPure, Category = "Utilities", meta = (Keywords = "unproject"))
	static bool DeprojectScreenToWorld(APlayerController const* Player, const FVector2D& ScreenPosition, FVector& WorldPosition, FVector& WorldDirection);

	/** 
	 * Transforms the given 3D world-space point into a its 2D screen space coordinate. 
	 * @param Player			Project using this player's view.
	 * @param WorldPosition		World position to project.
	 * @param ScreenPosition	(out) Corresponding 2D position in screen space
	 * @param bPlayerViewportRelative	Should this be relative to the player viewport subregion (useful when using player attached widgets in split screen)
	 */
	UFUNCTION(BlueprintPure, Category = "Utilities")
	static bool ProjectWorldToScreen(APlayerController const* Player, const FVector& WorldPosition, FVector2D& ScreenPosition, bool bPlayerViewportRelative = false);
    
    /**
	 * Plays a sound directly with no attenuation, perfect for UI sounds.
	 *
	 * * Fire and Forget.
	 * * Not Replicated.
	 * @param Sound - Sound to play.
	 * @param VolumeMultiplier - Multiplied with the volume to make the sound louder or softer.
	 * @param PitchMultiplier - Multiplies the pitch.
	 * @param ConcurrencySettings - Override concurrency settings package to play sound with
	 * @param StartTime - How far in to the sound to begin playback at
	 * @param ConcurrencySettings - Override concurrency settings package to play sound with
	 * @param OwningActor - The actor to use as the "owner" for concurrency settings purposes. Allows PlaySound calls to do a concurrency limit per owner.
	 */
	UFUNCTION(BlueprintCallable, BlueprintCosmetic, Category="Audio", meta=( WorldContext="WorldContextObject", AdvancedDisplay = "2", UnsafeDuringActorConstruction = "true" ))
	static void PlaySound2D(const UObject* WorldContextObject, USoundBase* Sound, float VolumeMultiplier = 1.f, float PitchMultiplier = 1.f, float StartTime = 0.f, USoundConcurrency* ConcurrencySettings = nullptr, AActor* OwningActor = nullptr);

##### The meaning of ProjectWorldToScreen's return value

Even when the Actor is in **LEFT BACK** or **RIGHT BACK** of Camera, `ProjectWorldToScreen` still would return true,  
when Actor is int **RIGHT BEHIND** of Camera, `ProjectWorldToScreen` still would return false.


