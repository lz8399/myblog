+++
title= "[UE4]Physics Animation Related"
date= "2019-01-24T20:40:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Physics", "Animation"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-007.jpg"
+++

Physics Asset Properties Reference  
<!--more-->
https://docs.unrealengine.com/en-US/Engine/Physics/PhAT/Reference

Editing Physics Asset Physics Bodies  
https://docs.unrealengine.com/en-us/Engine/Physics/PhAT/HowTo/EditPhATPhysicsBodies

PhysX Constraint User Guide  
https://docs.unrealengine.com/en-US/Engine/Physics/Constraints/ConstraintsUserGuide

Physics Asset Editor - Constraints Graph  
https://docs.unrealengine.com/en-us/Engine/Physics/PhAT/Graph

##### How to enable Clothing on Android Device

Steps

1, Enable `bCompileNvCloth` in source file `UEBuildAndroid.cs`:

	Target.bCompileNvCloth = true;
	
Source path:  
Engine\Source\Programs\UnrealBuildTool\Platform\Android\UEBuildAndroid.cs

2, Add `NvCloth` module in .Build.cs.

	using UnrealBuildTool;

	public class TestTP2 : ModuleRules
	{
		public TestTP2(ReadOnlyTargetRules Target) : base(Target)
		{
			PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

			PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "NvCloth" });
		}
	}
	
Reference  
NvCloth  
http://gameworksdocs.nvidia.com/NvCloth/1.1/index.html

Build Tools  
https://docs.unrealengine.com/en-us/Programming/BuildTools

***
`我的天空里没有太阳，总是黑夜，但并不暗，因为有东西代替了太阳。虽然没有太阳那么明亮，但对我来说已经足够。凭借着这份光，我便能把黑夜当成白天。我从来就没有太阳，所以不怕失去。——东野圭吾《白夜行》`
