+++
title= "[UE4]C++创建DecalComponent并附加到角色、吸附地面"
date= "2018-01-05T16:42:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "DecalComponent"]
+++

keywords：DecalComponent、贴花、C++

使用的贴花材质是UE4模版工程TopDown中的贴花材质：M_Cursor_Decal。

    if (FootRingComponent)
	{
		FootRingComponent = NewObject<UDecalComponent>(MyCharacter->GetRootComponent());
		if (FootRingComponent)
		{
			FootRingComponent->RegisterComponent();
			FootRingComponent->AttachToComponent(MyCharacter->GetRootComponent(), FAttachmentTransformRules::KeepRelativeTransform);

			UMaterial* Material = LoadObject<UMaterial>(NULL, TEXT("Material'/Game/Materials/Decal/M_Cursor_Decal.M_Cursor_Decal'"));
			if (Material)
			{
				FootRingComponent->SetDecalMaterial(Material);
				FootRingComponent->DecalSize = FVector(16.f, 128.f, 128.f);
				FootRingComponent->SetRelativeRotation(FRotator(90.f, 90.f, 90.f));
				FootRingComponent->SetRelativeLocation(FVector(0.f, 0.f, -90.f));
			}
		}
	}