+++
title= "[UE4]引擎源码分析之：StaticLoadObject"
date= "2018-02-03T23:06:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
draft= true
+++

从FStreamableManager::LoadSynchronous到FUObjectHashTables AddObject的堆栈：

    UE4Editor-CoreUObject.dll!HashObject(UObjectBase * Object) Line 904	
    UE4Editor-CoreUObject.dll!UObjectBase::AddObject(FName InName, EInternalObjectFlags InSetInternalFlags) Line 246	
    UE4Editor-CoreUObject.dll!UObjectBase::UObjectBase(UClass * InClass, EObjectFlags InFlags, EInternalObjectFlags InInternalFlags, UObject * InOuter, FName InName) Line 102	
    UE4Editor-CoreUObject.dll!StaticAllocateObject(UClass * InClass, UObject * InOuter, FName InName, EObjectFlags InFlags, EInternalObjectFlags InternalSetFlags, bool bCanRecycleSubobjects, bool * bOutRecycledSubobject) Line 2434	
    UE4Editor-CoreUObject.dll!StaticConstructObject_Internal(UClass * InClass, UObject * InOuter, FName InName, EObjectFlags InFlags, EInternalObjectFlags InternalSetFlags, UObject * InTemplate, bool bCopyTransientsFromClassDefaults, FObjectInstancingGraph * InInstanceGraph, bool bAssumeTemplateIsArchetype) Line 3161	
    [Inline Frame] UE4Editor-CoreUObject.dll!NewObject(UObject * Outer, FName) Line 1164	
    UE4Editor-CoreUObject.dll!CreatePackage(UObject * InOuter, const wchar_t * PackageName) Line 645	
    UE4Editor-CoreUObject.dll!GetPackageLinker(UPackage * InOuter, const wchar_t * InLongPackageName, unsigned int LoadFlags, UPackageMap * Sandbox, FGuid * CompatibleGuid) Line 642	
    UE4Editor-CoreUObject.dll!LoadPackageInternal(UPackage * InOuter, const wchar_t * InLongPackageNameOrFilename, unsigned int LoadFlags, FLinkerLoad * ImportLinker) Line 1240	
    UE4Editor-CoreUObject.dll!LoadPackage(UPackage * InOuter, const wchar_t * InLongPackageName, unsigned int LoadFlags) Line 1436	
    UE4Editor-CoreUObject.dll!ResolveName(UObject * & InPackage, FString & InOutName, bool Create, bool Throw, unsigned int LoadFlags) Line 792	
    UE4Editor-CoreUObject.dll!StaticLoadObjectInternal(UClass * ObjectClass, UObject * InOuter, const wchar_t * InName, const wchar_t * Filename, unsigned int LoadFlags, UPackageMap * Sandbox, bool bAllowObjectReconciliation) Line 880	
    UE4Editor-CoreUObject.dll!StaticLoadObject(UClass * ObjectClass, UObject * InOuter, const wchar_t * InName, const wchar_t * Filename, unsigned int LoadFlags, UPackageMap * Sandbox, bool bAllowObjectReconciliation) Line 947	
    UE4Editor-Engine.dll!FStreamableManager::StreamInternal(const FSoftObjectPath & InTargetName, int Priority, TSharedRef<FStreamableHandle,0> Handle) Line 786	
    UE4Editor-Engine.dll!FStreamableManager::StartHandleRequests(TSharedRef<FStreamableHandle,0> Handle) Line 989	
    UE4Editor-Engine.dll!FStreamableManager::RequestAsyncLoad(const TArray<FSoftObjectPath,FDefaultAllocator> & TargetsToStream, TBaseDelegate<void> DelegateToCall, int Priority, bool bManageActiveHandle, bool bStartStalled, const FString & DebugName) Line 936	
    UE4Editor-Engine.dll!FStreamableManager::RequestSyncLoad(const TArray<FSoftObjectPath,FDefaultAllocator> & TargetsToStream, bool bManageActiveHandle, const FString & DebugName) Line 962	
    UE4Editor-Engine.dll!FStreamableManager::RequestSyncLoad(const FSoftObjectPath & TargetToStream, bool bManageActiveHandle, const FString & DebugName) Line 979	
    UE4Editor-Engine.dll!FStreamableManager::LoadSynchronous(const FSoftObjectPath & Target, bool bManageActiveHandle, TSharedPtr<FStreamableHandle,0> * RequestHandlePointer) Line 1012	

UObject从ConditionalCollectGarbage到FUObjectHashTables RemoveObject的堆栈
        
    UE4Editor-CoreUObject.dll!UnhashObject(UObjectBase * Object) Line 934	
    UE4Editor-CoreUObject.dll!UObjectBase::LowLevelRename(FName NewName, UObject * NewOuter) Line 259	
    UE4Editor-CoreUObject.dll!UObject::BeginDestroy() Line 721	
    UE4Editor-CoreUObject.dll!UObject::ConditionalBeginDestroy() Line 884	
    UE4Editor-CoreUObject.dll!CollectGarbageInternal(EObjectFlags KeepFlags, bool bPerformFullPurge) Line 1496	
    UE4Editor-CoreUObject.dll!TryCollectGarbage(EObjectFlags KeepFlags, bool bPerformFullPurge) Line 1560	
    UE4Editor-Engine.dll!UEngine::ConditionalCollectGarbage() Line 1072	
    UE4Editor-Engine.dll!UWorld::Tick(ELevelTick TickType, float DeltaSeconds) Line 1612	
    UE4Editor-UnrealEd.dll!UEditorEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 1481	
    UE4Editor-UnrealEd.dll!UUnrealEdEngine::Tick(float DeltaSeconds, bool bIdleMode) Line 401	
    UE4Editor.exe!FEngineLoop::Tick() Line 3320	
    [Inline Frame] UE4Editor.exe!EngineTick() Line 62	
