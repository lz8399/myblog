+++
title= "[UE4]LNK2019 unresolved external symbol - GetPrivateStaticClass"
date= "2018-10-14T21:02:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Plugin", "LNK2019", "GetPrivateStaticClass"]
+++

UE4 Plugin Link Error:

    Error	LNK2019	unresolved external symbol "private: static class UClass * __cdecl UMyComponent::GetPrivateStaticClass(void)" (?GetPrivateStaticClass@UMyComponent@@CAPEAVUClass@@XZ) referenced in function "class UMyComponent * __cdecl NewObject<class UMyComponent>(class UObject *)" (??$NewObject@VUMyComponent@@@@YAPEAVUMyComponent@@PEAVUObject@@@Z)	ClimbWall	

Reason:  
Maybe you removed UE4's macro in your header.
    
Solution:  
Add UE4 stylized macro in header, e.g.:
    
    UCLASS()
    class TESTPLUGIN_API UMyComponent : public UActorComponent
    {
        GENERATED_BODY()
	}