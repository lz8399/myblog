+++
title= "[UE4]DestructibleComponent doesn't respect to Collision change"
date= "2018-10-30T12:18:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "DestructibleComponent", "Collision"]
+++

Problem:  
There's a bug that DestructibleComponent isn't affectd by `SetActorEnableCollision` or `SetCollisionEnabled`.

Solution:  
Add a custom Component inherit from DestructibleComponent, then override two functions: `OnActorEnableCollisionChanged`, `SetCollisionEnabled`

    // Copyright 2015 inbetweengames

    #include "ProjectDisco.h"
    #include "DADestructibleComponent.h"


    void UDADestructibleComponent::OnActorEnableCollisionChanged()
    {
        // Update physical properties of the chunks in the mesh if the body instance is valid
        FBodyInstance* BodyInst = GetBodyInstance();
        if (BodyInst)
        {
            BodyInst->UpdatePhysicsFilterData();
        }

        // Update physical properties for individual bone instances as well
        if (SkeletalMesh)
        {
            int32 NumBones = SkeletalMesh->RefSkeleton.GetNum();
            for (int32 BoneIdx = 0; BoneIdx < NumBones; ++BoneIdx)
            {
                FName BoneName = SkeletalMesh->RefSkeleton.GetBoneName(BoneIdx);
                FBodyInstance* Instance = GetBodyInstance(BoneName);
                if (Instance)
                {
                    Instance->UpdatePhysicsFilterData();
                }
            }
        }

        Super::OnActorEnableCollisionChanged();
    }

    void UDADestructibleComponent::SetCollisionEnabled(ECollisionEnabled::Type NewType)
    {
        // Update physical properties of the chunks in the mesh if the body instance is valid
        FBodyInstance* BodyInst = GetBodyInstance();
        if (BodyInst && BodyInst->GetCollisionEnabled() != NewType)
        {
            BodyInst->SetCollisionEnabled(NewType);
        }

        // Update physical properties for individual bone instances as well
        if (SkeletalMesh)
        {
            int32 NumBones = SkeletalMesh->RefSkeleton.GetNum();
            for (int32 BoneIdx = 0; BoneIdx < NumBones; ++BoneIdx)
            {
                FName BoneName = SkeletalMesh->RefSkeleton.GetBoneName(BoneIdx);
                FBodyInstance* Instance = GetBodyInstance(BoneName);
                if (Instance && Instance->GetCollisionEnabled() != NewType)
                {
                    Instance->SetCollisionEnabled(NewType);
                }
            }
        }

        Super::SetCollisionEnabled(NewType);
    }
    
##### Reference
DestructibleComponent does not respect calls to UPrimitiveComponent::SetCollisionEnabled or AActor::SetActorEnableCollision at runtime  
https://answers.unrealengine.com/questions/354110/view.html
