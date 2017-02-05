+++
title= "[UE4]如何遍历场景中的所有Actor和Object(CPP)"
date= "2016-09-29T19:43:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

原文：
https://wiki.unrealengine.com/Iterators:_Object_%26_Actor_Iterators,_Optional_Class_Scope_For_Faster_Search

遍历所有SkeletalMeshComponent

    for ( TObjectIterator<USkeletalMeshComponent> Itr; Itr; ++Itr )
    {
        // Access the subclass instance with the * or -> operators.
        USkeletalMeshCompoment *Component = *Itr;
        ClientMessage(Itr->GetName());
    }

遍历所有StaticMeshActor

    for (TActorIterator<AStaticMeshActor> ActorItr(GetWorld()); ActorItr; ++ActorItr)
    {
        // Same as with the Object Iterator, access the subclass instance with the * or -> operators.
        AStaticMeshActor *Mesh = *ActorItr;
        ClientMessage(ActorItr->GetName());
        ClientMessage(ActorItr->GetActorLocation().ToString());
    }

遍历所有Character

    for (TActorIterator<ACharacter> ActorItr(GetWorld()); ActorItr; ++ActorItr)
    {
        if (ActorItr->GetName().Contains("beiminghuoque"))
        {
            AMyCharacter* Warrior = (AMyCharacter*)*ActorItr;
            FString msg = FString::Printf(TEXT("#########:%d"), (int)Warrior->State());
            GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Red, msg);
        }
    }

遍历所有自定义Character：

    for (TActorIterator<AMyCharacter> ActorItr(GetWorld()); ActorItr; ++ActorItr)
    {	
    }