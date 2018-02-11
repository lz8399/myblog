+++
title= "[UE4]如何遍历场景中的所有Actor和Object(C++)"
date= "2017-12-26T22:01:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "VisualStudio"]
+++

如果用以下方式遍历：

	for (TObjectIterator<AWarSoulCharacter> Itr; Itr; ++Itr)
	
则当编辑器中打开蓝图后（双击蓝图），该蓝图也会出被遍历出来。不打开则不在遍历范围内。

诡异效果：
{{< figure src="/img/20171226-[UE4]如何遍历场景中的所有Actor和Object(C++)/[UE4]如何遍历场景中的所有Actor和Object(C++)-01.jpg">}}


这两种不会

	for (FConstPawnIterator Itr = GetWorld()->GetPawnIterator(); Itr; ++Itr)
	
	for (TActorIterator<AWarSoulCharacter> ActorItr(GetWorld()); ActorItr; ++ActorItr)

其他未测试。