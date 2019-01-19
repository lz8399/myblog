+++
title= "[UE4]Transform skeletal bone in C++"
date= "2019-01-05T21:29:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "skeletal bone", "Transform"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-018.jpg"
+++

##### Blueprint
<!--more-->

Blueprint Node

	Transform Bone
	
Example

{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-01.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-02.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-03.jpg">}}
	
##### PoseableMeshComponent of C++ 

Steps

1. Add `UPoseableMeshComponent` in your Actor class, and set Skeletal Mesh asset for it.
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-04.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-05.jpg">}}
{{< alert info >}}
Because the transformation of PoseableMeshComponent is entirely be handle by user, so there's no property to set the Animation Blueprint.
{{< /alert >}}
2. Modify bones transform by UPoseableMeshComponent's functions:

		UFUNCTION(BlueprintCallable, Category="Components|PoseableMesh")
		void SetBoneTransformByName(FName BoneName, const FTransform& InTransform, EBoneSpaces::Type BoneSpace);

		UFUNCTION(BlueprintCallable, Category="Components|PoseableMesh")
		void SetBoneLocationByName(FName BoneName, FVector InLocation, EBoneSpaces::Type BoneSpace);

		UFUNCTION(BlueprintCallable, Category="Components|PoseableMesh")
		void SetBoneRotationByName(FName BoneName, FRotator InRotation, EBoneSpaces::Type BoneSpace);

		UFUNCTION(BlueprintCallable, Category="Components|PoseableMesh")
		void SetBoneScaleByName(FName BoneName, FVector InScale3D, EBoneSpaces::Type BoneSpace);
		
##### SkeletalMeshComponent of C++ 

Sorry, I didn't find a way to transform bones of SkeletalMesh using C++.

##### Reference

Transform skeletal bone in C++  
https://answers.unrealengine.com/questions/59010/transform-skeletal-bone-in-c.html

Transform Bone  
https://docs.unrealengine.com/en-us/Engine/Animation/NodeReference/SkeletalControls/TransformBone

#### Bone Related

Transform a location/rotation in bone relative space to world space.

	Transform from Bone Space
	
Transform a location/rotation from world space to bone relative space.  
This is handy if you know the location in world space for a bone attachment, as AttachComponent takes location/rotation in bone-relative space.

	TransformToBoneSpace
	
C++

	void USkinnedMeshComponent::TransformToBoneSpace(FName BoneName, FVector InPosition, FRotator InRotation, FVector& OutPosition, FRotator& OutRotation) const
	
	void USkinnedMeshComponent::TransformFromBoneSpace(FName BoneName, FVector InPosition, FRotator InRotation, FVector& OutPosition, FRotator& OutRotation)
	
##### Problem Summary

If you want to control transform of bones at real-time, following properties may be set:

	// prevent anim frame skipping optimization based on visibility etc
	Mesh->bEnableUpdateRateOptimizations = false;

	// update animation even when mesh is not visible
	Mesh->MeshComponentUpdateFlag = EMeshComponentUpdateFlag::AlwaysTickPoseAndRefreshBones;

***
`发生过的事，以后还会发生；做过的事，将来还要再做。太阳底下没有新的事。有谁能说，看，这是新事？不，在我们出生之前早就有了。以往的事没有人去追忆，今后的事也没有人去掛念。 ──《旧约·传道书》`