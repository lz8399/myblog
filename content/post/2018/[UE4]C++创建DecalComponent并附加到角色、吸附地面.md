+++
title= "[UE4]C++创建DecalComponent并附加到角色、吸附地面"
date= "2018-01-05T16:42:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "DecalComponent"]
+++

keywords：DecalComponent、贴花、C++

使用的贴花材质是UE4模版工程TopDown中的贴花材质：M_Cursor_Decal。

    if (!FootRingComponent)
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
				FootRingComponent->SetRelativeRotation(FRotator(-90.f, 0.f, 0.f));
				FootRingComponent->SetRelativeLocation(FVector(0.f, 0.f, -90.f));
			}
		}
	}
    
{{< alert danger >}}
RelativeRotation一定要设置为FRotator(-90.f, 0.f, 0.f)或者FRotator(90.f, 90.f, 90.f)，否则贴花的无法正常显示；前者表示正向显示，后者表示反向显示。DecalSize的X表示贴花作用高度：比如一面墙高500，X设置为200，那么贴花在墙面上的显示高度只到200高度；Y、Z表示长和宽。
{{< /alert >}}

***
`我只是个戏子，在别人的故事里，流着自己的泪。----席慕蓉《戏子》`