+++
title= "[UE4]PlayerController常用API"
date= "2016-06-19T10:31:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

##### 获取当前的Pawn
一个Controller（包括AIController）只能同时possess一个Pawn。所以GetPawn()返回的就是当前控制的Pawn：

    APawn* Pawn = PC->GetPawn();
    
##### Screen相关

    //Convert 2D screen position to World Space 3D position and direction. Returns false if unable to determine value.
    bool DeprojectScreenPositionToWorld(float ScreenX, float ScreenY, FVector& WorldLocation, FVector& WorldDirection) const;
    
    /** Returns hit results from doing a collision query at a certain location on the screen */
	bool GetHitResultAtScreenPosition(const FVector2D ScreenPosition, const ECollisionChannel TraceChannel, const FCollisionQueryParams& CollisionQueryParams, FHitResult& HitResult) const;
    
    /**
	 * Returns the PlayerState associated with the player at the specified index.
	 * @param	PlayerIndex		the index [into the local player's GamePlayers array] for the player PlayerState to find
	 * @return	the PlayerState associated with the player at the specified index, or None if the player is not a split-screen player or
	 *			the index was out of range.
	 */
	class APlayerState* GetSplitscreenPlayerByIndex(int32 PlayerIndex = 1) const;
    
    
	/**
	 * After successful world to screen projection, allows custom post-processing of the resulting ScreenLocation.
	 * @return Whether projected location remains valid.
	 */
	virtual bool PostProcessWorldToScreen(FVector WorldLocation, FVector2D& ScreenLocation, bool bPlayerViewportRelative) const;
    
    
	/**
	 * Convert a World Space 3D position into a 2D Screen Space position.
	 * @return true if the world coordinate was successfully projected to the screen.
	 */
	bool ProjectWorldLocationToScreen(FVector WorldLocation, FVector2D& ScreenLocation, bool bPlayerViewportRelative = false) const;
    