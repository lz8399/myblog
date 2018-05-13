+++
title= "[UE4]LoadObject加载UAnimBlueprint失败"
date= "2018-04-14T22:10:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Math"]
+++

keywords：UE4、Dynamic Load、Animation Blueprint、LoadObject、动画蓝图

### 问题现象

假如用以下方式加载动画蓝图：

	FString AnimBPStringTest = "AnimBlueprint'/Game/ThirdPerson/Animations/ThirdPerson_AnimBP.ThirdPerson_AnimBP'";
	UAnimBlueprint* AnimationBP = LoadObject<UAnimBlueprint>(NULL, *AnimBPStringTest);

在PIE和Standalone模式下都可加载成功，但是一旦打包运行（打包配置中添加了该资源cook）就会加载失败，并提示如下错误：

	LogUObjectGlobals:Warning: Failed to find object 'AnimBlueprint /Game/ThirdPerson/Animations/ThirdPerson_AnimBP.ThirdPerson_AnimBP'
	
### 解决办法

貌似动画蓝图比较特殊，用LoadObject无法加载，如果要获取动画蓝图Class，可以通过如下方式加载：

	// get the blueprint class reference from the editor
	FString AnimClassStringTest = "Class'/Game/mixamo/Heidi/IcloneAnimBP.IcloneAnimBP_C'";

	// load the class
	UClass* AnimationClass = LoadObject<UClass>(NULL, *AnimClassStringTest);
	if (!AnimationClass) return;

	// assign the anim blueprint class to your skeletal mesh component
	Skeletal3DMeshComponent->SetAnimInstanceClass(AnimationClass);
	
参考：Why can't i dynamically load an animation BP in a packaged game  
https://answers.unrealengine.com/questions/263863/why-cant-i-dynamically-load-an-animation-bp-in-a-p.html


***
`二八佳人体似酥，腰间仗剑斩凡夫。虽然不见人头落，暗里教君骨髓枯。  ---唐·吕洞宾`
