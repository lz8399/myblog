+++
title= "[UE4]PlayerState用法"
date= "2018-01-13T14:08:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "PlayerState"]
+++

示例代码：

	const AYourPlayerController* PlayerPC = Cast<AYourPlayerController>(GetController());
	if (PlayerPC)
	{
		ATTSPlayerState* YourPlayerStateClass = Cast<ATTSPlayerState>(PlayerPC->PlayerState);
		if (YourPlayerStateClass)
		{
			GEngine->AddOnScreenDebugMessage(21, 1.0f, FColor::Red, FString::SanitizeFloat(YourPlayerStateClass->SomeVariable);
		}
	}
	
参考：PlayerState persistence across map change.  
https://answers.unrealengine.com/questions/43814/playerstate-persistence-across-map-change.html

