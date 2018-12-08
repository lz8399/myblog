+++
title= "[UE4]Slate and Native UMG(C++) Notes"
date= "2018-12-01T02:09:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UMG", "zoom"]
+++

##### How to scale or zoom a widget?

For Mouse Zoom:

+ override onMouseWheel
+ add Wheel Delta to Panning Canvas' Render Transform Scale
+ clamp min result to something above 0 (widgets flip if scaled below 0) and max to your desired max zoom
+ Set Render Scale of the Panning Canvas with the result of the above

Reference: How to scale/zoom a widget with blueprints?  
https://answers.unrealengine.com/questions/815202/how-to-scalezoom-a-widget-with-blueprints.html

##### How to clip widget display area?

Steps:

+ Add a CanvasPanel as the parent of your target widget
+ set the `Clipping` of CanvasPanel to `Clip to Bounds`

then the part outside CanvasPanel of your target widget would be clipped.

##### How to get the size of widget

Get actual size of widget:

    FVector2D UWidget::GetDesiredSize() const
  
Get size using slot:

    //ImgIcon is a UImage widget.
    if (UCanvasPanelSlot* Slot = Cast<UCanvasPanelSlot>(ImgIcon->Slot))
	{
		FVector2D Size = Slot->GetSize();
	}

Get size from Texture2D resource:
    
    //ImgIcon is a UImage widget.
    if (UTexture2D* Tex = Cast<UTexture2D>(ImgIcon->Brush.GetResourceObject()))
    {
        int32 X = Tex->GetSizeX();
    }
    
Using CachedGeometry:

    const FVector2D& IconLocSize = ImgIcon->GetCachedGeometry().GetLocalSize();
    const FVector2D& IconAbsSize = ImgIcon->GetCachedGeometry().GetAbsoluteSize();
    
##### How to get the position of widget

    //ImgIcon is a UImage widget.
    if (UCanvasPanelSlot* Slot = Cast<UCanvasPanelSlot>(ImgIcon->Slot))
	{
		FVector2D Pos = Slot->GetPosition();
	}

Using CachedGeometry:
    
    ImgIcon->GetCachedGeometry().GetAbsolutePosition();
    
##### How to get the screen size

    auto geometry = MyWidget->GetCachedGeometry();
    auto localSize = geometry.GetLocalSize();
    auto screenPosition = geometry.LocalToAbsolute(FVector2D(0, 0)); //TopLeft
    auto  screenSize = geometry.LocalToAbsolute(localSize) - screenPosition; // BotRight-TopLeft = real size

##### How to rotate a widget

code:

    void UWidget::SetRenderAngle(float Angle);  //Angle range: (-180, 180)
    
##### Mouse clicked position on widget

    FReply UMiniMapUI::NativeOnMouseButtonDown(const FGeometry& InGeometry, const FPointerEvent& InMouseEvent)
    {
        //Translates a screen position in pixels into the local space of a widget with the given geometry. 
        FVector2D ScreenPos;
        USlateBlueprintLibrary::ScreenToWidgetLocal(this, InGeometry, InMouseEvent.GetScreenSpacePosition(), ScreenPos);
    
        //Transforms AbsoluteCoordinate into the local space of this Geometry.
        FVector2D LocalWidgetMousePos = USlateBlueprintLibrary::AbsoluteToLocal(InGeometry, InMouseEvent.GetScreenSpacePosition());
        
        return FReply::Handled();
    }
    


