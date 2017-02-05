---
title: "[UE4]如何动态修改调整UMG组件的位置坐标(CPP和蓝图)"
date: "2016-10-18T23:48:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

蓝图：
{{< figure src="/img/20161018-[UE4]如何动态修改调整UMG组件的位置坐标(C++和蓝图).jpg">}}

C++：

    Cast<UCanvasPanelSlot>( MyBtn->Slot)->SetPosition(FVector2D(X, Y));

如果是全屏模式下，单单这一行代码没有问题，但是如果是窗口化模式，那么还需要处理DPI：

    // Call this once per-frame, on tick. To avoid re-calculation, or call it when settings / screen res changes.
    FORCEINLINE void ComputePlacementParams()
    {
        // Cache some of the shared parameters
        GetWorld()->GetGameViewport()->GetViewportSize(ViewportSize);
        ViewportCenter = ViewportSize / 2.f;

        // Root Panel Data
        CanvasSize = RootPanel_Ptr->GetDesiredSize();
        Divisor = CanvasSize / ViewportSize;
        DPIScaling = GetDefault<UUserInterfaceSettings>(UUserInterfaceSettings::StaticClass())->GetDPIScaleBasedOnSize(FIntPoint(ViewportSize.X, ViewportSize.Y));
    }


    // Called on tick to set location. 'IssScreenLocation' is the central position on-screen of where I want the widget.
    const FVector2D AnchorDivided = ((IssScreenLocation - ((ISSTrackerSlot_Ptr->GetSize() * DPIScaling) / 2.f)) * Divisor) / CanvasSize;
    const FAnchors NewAnchors = FAnchors(AnchorDivided.X, AnchorDivided.Y, AnchorDivided.X, AnchorDivided.Y);

    ISSTrackerSlot_Ptr->SetAnchors(NewAnchors);
    ISSTrackerSlot_Ptr->SetPosition(FVector2D::ZeroVector);	

需要的头文件：

    #include <Engine/UserInterfaceSettings.h>

