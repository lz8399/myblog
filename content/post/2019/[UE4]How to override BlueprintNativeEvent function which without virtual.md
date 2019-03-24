+++
title= "[UE4]How to override BlueprintNativeEvent function which without virtual"
date= "2019-03-24T16:49:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "BlueprintNativeEvent", "override"]
thumbnailImage= "/thumbnail/cover-Tso Moriri Lake.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++

Problem:  
<!--more-->
We want to override `CalculateBaseMagnitude` that without `virtual`:

	UFUNCTION(BlueprintNativeEvent, Category="Calculation")
	float CalculateBaseMagnitude(const FGameplayEffectSpec& Spec) const;
	
Solution:  
Before compilation, UnrealHeaderTool generates the virtual function for a BlueprintNativeEvent in the base class. The example from above would look like:

	virtual float CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const;

So in the derived C++ class, override (and implement) that function as usual in C++:

	class PROJECT_API UGMMCCustom : public UGameplayModMagnitudeCalculation
	{
		float CalculateBaseMagnitude_Implementation(const FGameplayEffectSpec& Spec) const override
		{
			return {}; // Add your custom implementation in the cpp file.
		}
	}

Reference  
https://stackoverflow.com/questions/55272245/how-to-override-a-blueprintnativeevent-function-in-c

***
`幸运的人一生都被童年治愈，不幸的人一生都在治愈童年。----阿德勒`

