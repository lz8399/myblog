+++
title= "[UE4]PackagingResults Error Bad name index"
date= "2018-12-01T02:09:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Packaging", "Error"]
+++

##### Package Error

    PackagingResults: Error: Bad name index -1/47
    
##### Solution 1
You can find the asset causing this by building the engine from source and adding breakpoints in these two place:
    
LinkerLoad.cpp

    void FLinkerLoad::BadNameIndexError(NAME_INDEX NameIndex)
    {
        UE_LOG(LogLinker, Error, TEXT("Bad name index %i/%i"), NameIndex, NameMap.Num());
    }

and

PackageReader.cpp

    FArchive& FPackageReader::operator<<( FName& Name )
    {
        check(Loader);

        NAME_INDEX NameIndex;
        FArchive& Ar = *this;
        Ar << NameIndex;

        if( !NameMap.IsValidIndex(NameIndex) )
        {
            UE_LOG(LogAssetRegistry, Fatal, TEXT("Bad name index %i/%i"), NameIndex, NameMap.Num() );
        }

        // if the name wasn't loaded (because it wasn't valid in this context)
        if (NameMap[NameIndex] == NAME_None)
        {
            int32 TempNumber;
            Ar << TempNumber;
            Name = NAME_None;
        }
        else
        {
            int32 Number;
            Ar << Number;
            // simply create the name from the NameMap's name and the serialized instance number
            Name = FName(NameMap[NameIndex], Number);
        }

        return *this;
    }

What does "bad name index -1/43" error mean in the context of a failed packaging attempt?
https://answers.unrealengine.com/questions/796763/what-does-bad-name-index-143-error-mean-in-the-con.html

##### Solution 2

Change `Cooker Progress Display Mode` to `Names and Remaining Packages` in **Project Setttings -> Engine -> Cooker**.  
than see the files name around the `Error: Bad name index`, check these files if is invaild.

