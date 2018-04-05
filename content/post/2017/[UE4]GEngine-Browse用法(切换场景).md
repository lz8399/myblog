+++
title= "[UE4]GEngine-Browse用法(切换场景)"
date= "2017-12-29T15:54:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Custom Shape Button"]
+++

代码示例：

	if (FWorldContext* Context = GEngine->GetWorldContextFromWorld(GetWorld()))
	{
		FString Error;
		FURL URL(TEXT("/Game/Demo/scecn_test/scecn_test02"));
		EBrowseReturnVal::Type RS = GEngine->Browse(*Context, URL, Error);
		if (EBrowseReturnVal::Type::Failure == RS)
		{
			WSI->ChangePlayerState(EPlayerState::EP_LoginFailed);
		}
	}
