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
    
##### 鼠标光标固定位置不动

假设需求如下：  
右键按住不放，屏幕转向，隐藏鼠标光标，松开右键时再显示鼠标光标，且鼠标光标的位置固定，不要跟随鼠标滑动而移动；  
左键按住不放，光标显示，且光标跟谁鼠标滑动而移动（比如RTS的框选操作）。

解决方案如下：

    void AMyPlayerController::OnLeftMousePressed()
    {
        //由于光标默认捕获规则是：Viewport中鼠标任意键的按下事件就会永久捕获。
        //FInputModeGameAndUI默认规则是：捕获时隐藏光标。所以这里需要修改捕获时不隐藏光标，否则按住左键不放时光标会一直隐藏。
        FInputModeGameAndUI InputMode;
        InputMode.SetHideCursorDuringCapture(false);
        
        SetInputMode(InputMode);
    }
    
    void AMyPlayerController::OnLeftMouseReleased()
    {
        //左键松开事件中不用做任何处理
    }
    
    void AMyPlayerController::OnRightMousePressed()
    {
        //PlayerController的变量，控制是否隐藏光标
        bShowMouseCursor = false;
        
        //自定义变量，用来标识是否按住右键
        bRightMouseHold = true;

        SetInputMode(FInputModeGameOnly());
    }
    
    void AMyPlayerController::OnRightMouseReleased()
    {
        bShowMouseCursor = true;
        
        bRightMouseHold = false;

        SetInputMode(FInputModeGameAndUI());
    }

修改光标的捕获规则模式：  
Project Settings -> Engine -> Input -> Viewport Properties -> Default Viewport Mouse Capture Mode.  
默认是： Capture Permanently Including Initial Mouse Down，表示鼠标任意键的按下事件捕获，且是永久捕获。
