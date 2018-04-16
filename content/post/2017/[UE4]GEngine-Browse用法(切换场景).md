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

{{< alert danger >}}
GEngine->Browse这种方式第一次打开场景时正常，如果第二次切换场景（比如从别的场景再切回原场景），则会导致程序崩溃。建议用：UGameplayStatics::OpenLevel(GetWorld(), TEXT("/Game/Map/TestMap")); 这种方式来回切场景不会出现崩溃问题。
{{< /alert >}}