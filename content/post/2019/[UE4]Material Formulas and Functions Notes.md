+++
title= "[UE4]Material Formulas and Functions Notes"
date= "2019-01-26T17:16:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Materials", "Formulas", "Functions"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-004.jpg"
+++

##### 2 Ways of `Create Dynamic Material Instance`
<!--more-->
1st way:

	UMaterialInstanceDynamic* UPrimitiveComponent::CreateDynamicMaterialInstance(int32 ElementIndex, class UMaterialInterface* SourceMaterial, FName OptionalName)

2nd way:
	
	class UMaterialInstanceDynamic* UKismetMaterialLibrary::CreateDynamicMaterialInstance(UObject* WorldContextObject, class UMaterialInterface* Parent, FName OptionalName)

***
`回忆，是一种内心的谣言。──斯蒂芬·金（StephenEdwinKing）《杜马岛》`