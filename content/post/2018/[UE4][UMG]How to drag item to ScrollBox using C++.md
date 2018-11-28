+++
title= "[UE4][UMG]How to drag item to ScrollBox using C++"
date= "2018-11-26T16:22:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UMG", "Drag", "C++", "Native"]
+++

override NativeOnDragDetected() in the class which is draping from.

example source:

    void UItemSlotWidget::NativeOnDragDetected(const FGeometry& InGeometry,
        const FPointerEvent& InMouseEvent,
        UDragDropOperation*& OutOperation)
    {
        Super::NativeOnDragDetected(InGeometry, InMouseEvent, OutOperation);
        RTS_PlayerController->SetInputMode_UI_Only();
        OutOperation = CreateItemDrag();
    }


    FReply UItemSlotWidget::NativeOnMouseButtonDown(const FGeometry & InGeometry, const FPointerEvent & InMouseEvent)
    {
        FReply reply = Super::NativeOnMouseButtonDown(InGeometry, InMouseEvent);
        SetTextToInformationBar();
        if (InMouseEvent.GetEffectingButton() == EKeys::LeftMouseButton) {
            reply.DetectDrag(TakeWidget(), EKeys::LeftMouseButton);
        }
        return reply;
    }

    UDragDropOperation* UItemSlotWidget::CreateItemDrag() const {
        auto drag_drop_operation = NewObject<UItemDrag>();
        if (RTS_PlayerController && !IsEmpty()) {
            RTS_PlayerController->DragDropOp_property = drag_drop_operation; // for garbage collector
            drag_drop_operation->DraggedItem = const_cast<UItemSlotWidget*>(this);
            drag_drop_operation->ItemImage = currentImage_Texture2D;

            auto DragVisual = CreateWidget<UDraggedItem>(RTS_PlayerController, URTS_FunctionLibrary::GetClassPtrOf_DraggedItem_BP());
            DragVisual->ImageOfDraggedItem = NewObject<UImage>();
            DragVisual->ImageOfDraggedItem->SetBrushFromTexture(currentImage_Texture2D);

            drag_drop_operation->DefaultDragVisual = DragVisual;
            drag_drop_operation->Pivot = EDragPivot::MouseDown;
        }
        return drag_drop_operation;
    }

Reference:  
https://github.com/absentje/UE4/blob/master/RTS_Game/Source/RTS_Game/Private/UI/Inventory/ItemSlotWidget.cpp