+++
title= "[UE4]引擎源码分析之：Load Object"
date= "2018-02-03T23:06:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
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

执行异步加载的接口：Engine\Source\Runtime\CoreUObject\Private\Serialization\AsyncLoading.cpp

    int32 LoadPackageAsync(const FString& InName, const FGuid* InGuid /*= nullptr*/, const TCHAR* InPackageToLoadFrom /*= nullptr*/, FLoadPackageAsyncDelegate InCompletionDelegate /*= FLoadPackageAsyncDelegate()*/, EPackageFlags InPackageFlags /*= PKG_None*/, int32 InPIEInstanceID /*= INDEX_NONE*/, int32 InPackagePriority /*= 0*/)
    {
        static bool bOnce = false;
        if (!bOnce && GEventDrivenLoaderEnabled)
        {
            bOnce = true;
            FGCObject::StaticInit(); // otherwise this thing is created during async loading, but not associated with a package
        }

        // The comments clearly state that it should be a package name but we also handle it being a filename as this function is not perf critical
        // and LoadPackage handles having a filename being passed in as well.
        FString PackageName;
        if (FPackageName::IsValidLongPackageName(InName, /*bIncludeReadOnlyRoots*/true))
        {
            PackageName = InName;
        }
        // PackageName got populated by the conditional function
        else if (!(FPackageName::IsPackageFilename(InName) && FPackageName::TryConvertFilenameToLongPackageName(InName, PackageName)))
        {
            // PackageName will get populated by the conditional function
            FString ClassName;
            if (!FPackageName::ParseExportTextPath(PackageName, &ClassName, &PackageName))
            {
                UE_LOG(LogStreaming, Fatal, TEXT("LoadPackageAsync failed to begin to load a package because the supplied package name was neither a valid long package name nor a filename of a map within a content folder: '%s'"), *PackageName);
            }
        }

        FString PackageNameToLoad(InPackageToLoadFrom);
        if (PackageNameToLoad.IsEmpty())
        {
            PackageNameToLoad = PackageName;
        }
        // Make sure long package name is passed to FAsyncPackage so that it doesn't attempt to 
        // create a package with short name.
        if (FPackageName::IsShortPackageName(PackageNameToLoad))
        {
            UE_LOG(LogStreaming, Fatal, TEXT("Async loading code requires long package names (%s)."), *PackageNameToLoad);
        }

        if ( FCoreDelegates::OnAsyncLoadPackage.IsBound() )
        {
            FCoreDelegates::OnAsyncLoadPackage.Broadcast(InName);
        }

        // Generate new request ID and add it immediately to the global request list (it needs to be there before we exit
        // this function, otherwise it would be added when the packages are being processed on the async thread).
        const int32 RequestID = GPackageRequestID.Increment();
        FAsyncLoadingThread::Get().AddPendingRequest(RequestID);

        // Allocate delegate on Game Thread, it is not safe to copy delegates by value on other threads
        TUniquePtr<FLoadPackageAsyncDelegate> CompletionDelegatePtr;
        if (InCompletionDelegate.IsBound())
        {
            CompletionDelegatePtr.Reset(new FLoadPackageAsyncDelegate(InCompletionDelegate));
        }

        // Add new package request
        FAsyncPackageDesc PackageDesc(RequestID, *PackageName, *PackageNameToLoad, InGuid ? *InGuid : FGuid(), MoveTemp(CompletionDelegatePtr), InPackageFlags, InPIEInstanceID, InPackagePriority);
        FAsyncLoadingThread::Get().QueuePackage(PackageDesc);

        return RequestID;
    }
    
***
`过寡，众相害之；超凡，则群相仰之。`