+++
title= "[UE4]Transform skeletal bone in C++"
date= "2019-01-05T21:29:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "skeletal bone", "Transform"]
thumbnailImage= "/thumbnail/cover-japan-001.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++
Add `UPoseableMeshComponent` in your Actor class, and set Skeletal Mesh asset for it.  
Modify bones transform by UPoseableMeshComponent's functions:
<!--more-->

##### Blueprint Node

	Transform from Bone Space
	
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-01.jpg">}}
	
##### C++ code

Steps

1. Add `UPoseableMeshComponent` in your Actor class, and set Skeletal Mesh asset for it.
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-02.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-03.jpg">}}
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

##### Reference

Transform skeletal bone in C++  
https://answers.unrealengine.com/questions/59010/transform-skeletal-bone-in-c.html