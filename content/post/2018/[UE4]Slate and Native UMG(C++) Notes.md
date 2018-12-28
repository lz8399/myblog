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
    
Usage of `GetDesiredSize`:

    void UMyWidget::AddToScreen(ULocalPlayer* LocalPlayer, int32 ZOrder)
    {
        Super::AddToScreen(LocalPlayer, ZOrder);

        Super::ForceLayoutPrepass();

        FVector2D Size = GetDesiredSize();
    }
    
{{< alert danger >}}
`GetDesiredSize()` isn't usable before `NativeTick()` triggered, if you want to get the widget size when widget initilized, you need to call function ` Super::ForceLayoutPrepass()`. If you add a child in widget and want to show it on viewport in this frame, you also need to call this function too.
{{< /alert >}}

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
    
##### How to set the size of widget
    
    //ImgIcon is a UImage widget.
    if (UCanvasPanelSlot* Slot = Cast<UCanvasPanelSlot>(ImgIcon->Slot))
	{
		Slot->SetSize(FVector2D(100.f, 100.f));
	}
    
##### How to set the size of UserWidget(whole UMG UI)

    void UUserWidget::SetDesiredSizeInViewport(FVector2D DesiredSize);
    
##### How to get the position of widget

    //ImgIcon is a UImage widget.
    if (UCanvasPanelSlot* Slot = Cast<UCanvasPanelSlot>(ImgIcon->Slot))
	{
		FVector2D Pos = Slot->GetPosition();
	}

Using CachedGeometry:
    
    ImgIcon->GetCachedGeometry().GetAbsolutePosition();
    
##### How to set the position of widget

    void UWidget::SetRenderTranslation(FVector2D Translation)
    
##### How to set the position of UserWidget

    void UUserWidget::SetPositionInViewport(FVector2D Position, bool bRemoveDPIScale )
    
##### How to scale the widget

    void UWidget::SetRenderScale(FVector2D Scale)
    
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
    
### UWidgetLayoutLibrary

##### How to get the scale of viewport

    FVector2D UWidgetLayoutLibrary::GetViewportScale(UObject* WorldContextObject);
    
##### How to get the viewport size

    FVector2D UWidgetLayoutLibrary::GetViewportSize(UObject* WorldContextObject);

##### How to get the Geometry of all widgets in Viewport or PlayerScreen

    FGeometry UWidgetLayoutLibrary::GetViewportWidgetGeometry(UObject* WorldContextObject);
    
    FGeometry UWidgetLayoutLibrary::GetPlayerScreenWidgetGeometry(APlayerController* PlayerController);
    
##### How to get mouse position

    //Gets the platform's mouse cursor position.  This is the 'absolute' desktop location of the mouse.
    FVector2D UWidgetLayoutLibrary::GetMousePositionOnPlatform();
    
    //Gets the platform's mouse cursor position in the local space of the viewport widget.
    FVector2D UWidgetLayoutLibrary::GetMousePositionOnViewport(UObject* WorldContextObject);
    
##### How to removes all widgets from the viewport
    
    void UWidgetLayoutLibrary::RemoveAllWidgets(UObject* WorldContextObject);
   
##### How to alter widget self's anchor to the center of itself.

Put the widget into a UCanvasPanel, then set Alignment of this UCanvasPanel as (0.5f, 0.5f):

	CanvasPanelSlot->SetAlignment(FVector2D(0.5f, 0.5f));

##### How to fade in / out widget

Event for fade begin:

	LerpTime = 0.f;
	LerpDuration = 1.5f;

	FLinearColor SrcColor = MyTextBlock->ColorAndOpacity.GetSpecifiedColor();
	FLinearColor DestColor = SrcColor;
	DestColor.A = 0.f;
	
in Tick()
	
	if (LerpTime < LerpDuration)
	{
		LerpTime += DeltaSeconds;

		FLinearColor Color = FMath::Lerp<FLinearColor>(SrcColor, DestColor, LerpTime / LerpDuration);

		MyTextBlock->SetColorAndOpacity(Color);
	}