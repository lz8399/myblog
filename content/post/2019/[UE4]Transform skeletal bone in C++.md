+++
title= "[UE4]Transform skeletal bone in C++"
date= "2019-01-05T21:29:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "skeletal bone", "Transform"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-018.jpg"
+++

##### Transform SkeletalMeshComponent's bone in Blueprint
<!--more-->

Blueprint Node

	Transform (Modify) Bone
	
Example

{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-01.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-02.jpg">}}
{{< figure src="/img/20190105-[UE4]Transform skeletal bone in C++/[UE4]Transform skeletal bone in C++-03.jpg">}}
	
##### Transform PoseableMeshComponent's bone in C++ 

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
		
##### Transform SkeletalMeshComponent's bone in C++

Reference by Engine source: 

Engine\Source\Editor\AnimGraph\Classes\AnimGraphNode_ModifyBone.h  
{{< alert success >}}
This is the GraphNode `Transform (Modify) Bone` in Animation Blueprint Editor. The property `FAnimNode_ModifyBone` is the definite native class for transforming bones.
{{< /alert >}}
	
	UCLASS(meta=(Keywords = "Modify Transform"))
	class ANIMGRAPH_API UAnimGraphNode_ModifyBone : public UAnimGraphNode_SkeletalControlBase
	{
		GENERATED_UCLASS_BODY()

		UPROPERTY(EditAnywhere, Category=Settings)
		FAnimNode_ModifyBone Node;

	public:
		// UEdGraphNode interface
		virtual FText GetNodeTitle(ENodeTitleType::Type TitleType) const override;
		virtual FText GetTooltipText() const override;
		// End of UEdGraphNode interface

	protected:
		// UAnimGraphNode_Base interface
		virtual void ValidateAnimNodeDuringCompilation(USkeleton* ForSkeleton, FCompilerResultsLog& MessageLog) override;
		virtual FEditorModeID GetEditorMode() const override;
		virtual void CopyNodeDataToPreviewNode(FAnimNode_Base* InPreviewNode) override;
		virtual void CopyPinDefaultsToNodeData(UEdGraphPin* InPin) override;
		// End of UAnimGraphNode_Base interface

		// UAnimGraphNode_SkeletalControlBase interface
		virtual FText GetControllerDescription() const override;
		virtual const FAnimNode_SkeletalControlBase* GetNode() const override { return &Node; }
		// End of UAnimGraphNode_SkeletalControlBase interface

	private:
		/** Constructing FText strings can be costly, so we cache the node's title */
		FNodeTitleTextTable CachedNodeTitles;

		// storing current widget mode 
		int32 CurWidgetMode;
	};

Engine\Source\Runtime\AnimGraphRuntime\Public\BoneControllers\AnimNode_ModifyBone.h

	UENUM()
	enum EBoneModificationMode
	{
		/** The modifier ignores this channel (keeps the existing bone translation, rotation, or scale). */
		BMM_Ignore UMETA(DisplayName = "Ignore"),

		/** The modifier replaces the existing translation, rotation, or scale. */
		BMM_Replace UMETA(DisplayName = "Replace Existing"),

		/** The modifier adds to the existing translation, rotation, or scale. */
		BMM_Additive UMETA(DisplayName = "Add to Existing")
	};

	/**
	 *	Simple controller that replaces or adds to the translation/rotation of a single bone.
	 */
	USTRUCT(BlueprintInternalUseOnly)
	struct ANIMGRAPHRUNTIME_API FAnimNode_ModifyBone : public FAnimNode_SkeletalControlBase
	{
		GENERATED_USTRUCT_BODY()

		/** Name of bone to control. This is the main bone chain to modify from. **/
		UPROPERTY(EditAnywhere, Category=SkeletalControl) 
		FBoneReference BoneToModify;

		/** New translation of bone to apply. */
		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Translation, meta=(PinShownByDefault))
		FVector Translation;

		/** New rotation of bone to apply. */
		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Rotation, meta=(PinShownByDefault))
		FRotator Rotation;

		/** New Scale of bone to apply. This is only worldspace. */
		UPROPERTY(EditAnywhere, BlueprintReadWrite, Category=Scale, meta=(PinShownByDefault))
		FVector Scale;

		/** Whether and how to modify the translation of this bone. */
		UPROPERTY(EditAnywhere, Category=Translation)
		TEnumAsByte<EBoneModificationMode> TranslationMode;

		/** Whether and how to modify the translation of this bone. */
		UPROPERTY(EditAnywhere, Category=Rotation)
		TEnumAsByte<EBoneModificationMode> RotationMode;

		/** Whether and how to modify the translation of this bone. */
		UPROPERTY(EditAnywhere, Category=Scale)
		TEnumAsByte<EBoneModificationMode> ScaleMode;

		/** Reference frame to apply Translation in. */
		UPROPERTY(EditAnywhere, Category=Translation)
		TEnumAsByte<enum EBoneControlSpace> TranslationSpace;

		/** Reference frame to apply Rotation in. */
		UPROPERTY(EditAnywhere, Category=Rotation)
		TEnumAsByte<enum EBoneControlSpace> RotationSpace;

		/** Reference frame to apply Scale in. */
		UPROPERTY(EditAnywhere, Category=Scale)
		TEnumAsByte<enum EBoneControlSpace> ScaleSpace;

		FAnimNode_ModifyBone();

		// FAnimNode_Base interface
		virtual void GatherDebugData(FNodeDebugData& DebugData) override;
		// End of FAnimNode_Base interface

		// FAnimNode_SkeletalControlBase interface
		virtual void EvaluateSkeletalControl_AnyThread(FComponentSpacePoseContext& Output, TArray<FBoneTransform>& OutBoneTransforms) override;
		virtual bool IsValidToEvaluate(const USkeleton* Skeleton, const FBoneContainer& RequiredBones) override;
		// End of FAnimNode_SkeletalControlBase interface

	private:
		// FAnimNode_SkeletalControlBase interface
		virtual void InitializeBoneReferences(const FBoneContainer& RequiredBones) override;
		// End of FAnimNode_SkeletalControlBase interface
	};

{{< alert success >}} `FAnimNode_ModifyBone` inherit from `FAnimNode_SkeletalControlBase` and implement father's function `EvaluateSkeletalControl_AnyThread` which execute transformation of bones{{< /alert >}}

	void FAnimNode_ModifyBone::EvaluateSkeletalControl_AnyThread(FComponentSpacePoseContext& Output, TArray<FBoneTransform>& OutBoneTransforms)
	{
		check(OutBoneTransforms.Num() == 0);

		// the way we apply transform is same as FMatrix or FTransform
		// we apply scale first, and rotation, and translation
		// if you'd like to translate first, you'll need two nodes that first node does translate and second nodes to rotate.
		const FBoneContainer& BoneContainer = Output.Pose.GetPose().GetBoneContainer();

		FCompactPoseBoneIndex CompactPoseBoneToModify = BoneToModify.GetCompactPoseIndex(BoneContainer);
		FTransform NewBoneTM = Output.Pose.GetComponentSpaceTransform(CompactPoseBoneToModify);
		FTransform ComponentTransform = Output.AnimInstanceProxy->GetComponentTransform();

		if (ScaleMode != BMM_Ignore)
		{
			// Convert to Bone Space.
			FAnimationRuntime::ConvertCSTransformToBoneSpace(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, ScaleSpace);

			if (ScaleMode == BMM_Additive)
			{
				NewBoneTM.SetScale3D(NewBoneTM.GetScale3D() * Scale);
			}
			else
			{
				NewBoneTM.SetScale3D(Scale);
			}

			// Convert back to Component Space.
			FAnimationRuntime::ConvertBoneSpaceTransformToCS(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, ScaleSpace);
		}

		if (RotationMode != BMM_Ignore)
		{
			// Convert to Bone Space.
			FAnimationRuntime::ConvertCSTransformToBoneSpace(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, RotationSpace);

			const FQuat BoneQuat(Rotation);
			if (RotationMode == BMM_Additive)
			{	
				NewBoneTM.SetRotation(BoneQuat * NewBoneTM.GetRotation());
			}
			else
			{
				NewBoneTM.SetRotation(BoneQuat);
			}

			// Convert back to Component Space.
			FAnimationRuntime::ConvertBoneSpaceTransformToCS(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, RotationSpace);
		}
		
		if (TranslationMode != BMM_Ignore)
		{
			// Convert to Bone Space.
			FAnimationRuntime::ConvertCSTransformToBoneSpace(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, TranslationSpace);

			if (TranslationMode == BMM_Additive)
			{
				NewBoneTM.AddToTranslation(Translation);
			}
			else
			{
				NewBoneTM.SetTranslation(Translation);
			}

			// Convert back to Component Space.
			FAnimationRuntime::ConvertBoneSpaceTransformToCS(ComponentTransform, Output.Pose, NewBoneTM, CompactPoseBoneToModify, TranslationSpace);
		}
		
		OutBoneTransforms.Add( FBoneTransform(BoneToModify.GetCompactPoseIndex(BoneContainer), NewBoneTM) );
	}

Reference: Creating Custom Animation Nodes  
https://www.unrealengine.com/en-US/blog/creating-custom-animation-nodes

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