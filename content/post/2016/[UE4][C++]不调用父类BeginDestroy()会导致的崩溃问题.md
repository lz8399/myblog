---
title: "[UE4][C++]不调用父类BeginDestroy()会导致的崩溃问题"
date: "2016-11-01T23:23:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Error
---


出现以下异常的原因是：重写了BeginDestroy()函数但没有在其内部执行`Super::BeginDestroy()`。

    Fatal error: [File:D:\Build\++UE4+Release-4.13+Compile\Sync\Engine\Source\Runtime\CoreUObject\Private\UObject\Obj.cpp] [Line: 742] 
    HPlayerController None.None:None.HPlayerController_0 failed to route BeginDestroy


    UE4Editor_Core!FDebug::AssertFailed() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\misc\outputdevice.cpp:421]
    UE4Editor_CoreUObject!UObject::ConditionalBeginDestroy() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\coreuobject\private\uobject\obj.cpp:742]
    UE4Editor_CoreUObject!CollectGarbageInternal() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\coreuobject\private\uobject\garbagecollection.cpp:1281]
    UE4Editor_CoreUObject!CollectGarbage() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\coreuobject\private\uobject\garbagecollection.cpp:1320]
    UE4Editor_UnrealEd!UEditorEngine::EndPlayMap() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\unrealed\private\playlevel.cpp:408]
    UE4Editor_LevelEditor!FLevelViewportLayout::~FLevelViewportLayout() [d:\build\++ue4+release-4.13+compile\sync\engine\source\editor\leveleditor\private\levelviewportlayout.cpp:145]
    UE4Editor_LevelEditor!FLevelViewportLayout2x2::`scalar deleting destructor'()
    UE4Editor_LevelEditor!FLevelViewportTabContent::~FLevelViewportTabContent()
    UE4Editor_LevelEditor!SharedPointerInternals::TReferenceControllerWithDeleter<FLevelViewportTabContent,SharedPointerInternals::DefaultDeleter<FLevelViewportTabContent> >::DestroyObject() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\templates\sharedpointerinternals.h:104]
    UE4Editor_LevelEditor!SViewportsOverlay::~SViewportsOverlay()
    UE4Editor_LevelEditor!SViewportsOverlay::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SBorder::`vector deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SOverlay::FOverlaySlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SOverlay::~SOverlay()
    UE4Editor_Slate!SOverlay::`scalar deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SBoxPanel::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SBoxPanel::~SBoxPanel()
    UE4Editor_Slate!SVerticalBox::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingTabStack::`vector deleting destructor'()
    UE4Editor_SlateCore!FSlotBase::~FSlotBase() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slatecore\private\slotbase.cpp:34]
    UE4Editor_Slate!TIndirectArray<SSplitter::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_Slate!SSplitter::~SSplitter()
    UE4Editor_Slate!SSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSlotBase::~FSlotBase() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slatecore\private\slotbase.cpp:34]
    UE4Editor_Slate!TIndirectArray<SSplitter::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_Slate!SSplitter::~SSplitter()
    UE4Editor_Slate!SSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSlotBase::~FSlotBase() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slatecore\private\slotbase.cpp:34]
    UE4Editor_Slate!TIndirectArray<SSplitter::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_Slate!SSplitter::~SSplitter()
    UE4Editor_Slate!SSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!FSlotBase::~FSlotBase() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slatecore\private\slotbase.cpp:34]
    UE4Editor_Slate!TIndirectArray<SSplitter::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_Slate!SSplitter::~SSplitter()
    UE4Editor_Slate!SSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SOverlay::FOverlaySlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SOverlay::~SOverlay()
    UE4Editor_Slate!SOverlay::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingArea::`vector deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SBoxPanel::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SBoxPanel::~SBoxPanel()
    UE4Editor_LevelEditor!SVerticalBox::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_LevelEditor!SLevelEditor::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SBorder::`vector deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SOverlay::FOverlaySlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SOverlay::~SOverlay()
    UE4Editor_Slate!SOverlay::`scalar deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SBoxPanel::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SBoxPanel::~SBoxPanel()
    UE4Editor_Slate!SVerticalBox::`scalar deleting destructor'()
    UE4Editor_SlateCore!FSimpleSlot::~FSimpleSlot()
    UE4Editor_SlateCore!SCompoundWidget::~SCompoundWidget()
    UE4Editor_Slate!SDockingTabStack::`vector deleting destructor'()
    UE4Editor_SlateCore!FSlotBase::~FSlotBase() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slatecore\private\slotbase.cpp:34]
    UE4Editor_Slate!TIndirectArray<SSplitter::FSlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_Slate!SSplitter::~SSplitter()
    UE4Editor_Slate!SSplitter::`vector deleting destructor'()
    UE4Editor_SlateCore!TIndirectArray<SOverlay::FOverlaySlot,FDefaultAllocator>::DestructAndFreeItems() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:3474]
    UE4Editor_SlateCore!SOverlay::~SOverlay()
    UE4Editor_Slate!SOverlay::`scalar deleting destructor'()
    UE4Editor_SlateCore!TArray<FArrangedWidget,TInlineAllocator<16,FDefaultAllocator> >::~TArray<FArrangedWidget,TInlineAllocator<16,FDefaultAllocator> >() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\public\containers\array.h:752]
    UE4Editor_Slate!FSlateApplication::RoutePointerUpEvent() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slate\private\framework\application\slateapplication.cpp:4974]
    UE4Editor_Slate!FSlateApplication::ProcessMouseButtonUpEvent() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slate\private\framework\application\slateapplication.cpp:5348]
    UE4Editor_Slate!FSlateApplication::OnMouseUp() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\slate\private\framework\application\slateapplication.cpp:5328]
    UE4Editor_Core!FWindowsApplication::ProcessDeferredMessage() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\windows\windowsapplication.cpp:1584]
    UE4Editor_Core!FWindowsApplication::DeferMessage() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\windows\windowsapplication.cpp:1930]
    UE4Editor_Core!FWindowsApplication::ProcessMessage() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\windows\windowsapplication.cpp:747]
    UE4Editor_Core!FWindowsApplication::AppWndProc() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\windows\windowsapplication.cpp:669]
    user32
    user32
    UE4Editor_Core!FWindowsPlatformMisc::PumpMessages() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\core\private\windows\windowsplatformmisc.cpp:905]
    UE4Editor!FEngineLoop::Tick() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\launchengineloop.cpp:2788]
    UE4Editor!GuardedMain() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\launch.cpp:156]
    UE4Editor!GuardedMainWrapper() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:126]
    UE4Editor!WinMain() [d:\build\++ue4+release-4.13+compile\sync\engine\source\runtime\launch\private\windows\launchwindows.cpp:202]
    UE4Editor!__scrt_common_main_seh() [f:\dd\vctools\crt\vcstartup\src\startup\exe_common.inl:264]
    kernel32
    ntdll
