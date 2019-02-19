+++
title= "[UE4]fatal error C1083 Cannot open include file 'FoliageType.generated.h"
date= "2019-02-18T14:34:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Foliage"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-014.jpg"
+++

##### Issue
<!--more-->
Compilation Error:

	fatal error C1083 Cannot open include file 'FoliageType.generated.h
	
Solution:  
Add `Foliage` in `PublicDependencyModuleNames` of *.Build.cs, e.g.

	public TestProj(ReadOnlyTargetRules Target) : base(Target)
	{
		PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

		PublicDependencyModuleNames.AddRange(new string[] { "Core", "CoreUObject", "Engine", "InputCore", "Foliage" });
	}
	
##### Reference

Fatal Error C1083: Cannot open include file: ‘xxx.generated.h’: No such file or directory Unreal Engine 4 Plugins  
http://www.mycmessia.com/2017/09/12/fatal-error-c1083-cannot-open-include-file-xxx-generated-h-no-file-directory-unreal-engine-4-plugins/

***
`一对年老夫妇，一起走过大半辈子，多年来他们每晚睡前最后一刻必定会跟对方说一句：我爱你。别人问他们为什么有这个习惯，丈夫说：我们都这把年纪了，这样做是为了保证，假如我们其中一个第二天没有醒来，我们在人生里留给对方最后一句说话就是这三个字。`

