+++
title= "[UE4]获取本地(Local)PlayerController的几种方式"
date= "2017-12-30T17:40:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "C++", "PlayerController"]
+++

代码：

	APlayerController* PC1 = GetWorld()->GetFirstLocalPlayerFromController()->GetPlayerController(GetWorld());
	APlayerController* PC2 = GetWorld()->GetFirstPlayerController();
	APlayerController* PC3 = GEngine->GetFirstLocalPlayerController(GetWorld());
    
***
`心似平原走马，易放难收。----《增广贤文》`