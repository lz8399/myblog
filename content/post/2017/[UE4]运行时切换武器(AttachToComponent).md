+++
title= "[UE4]运行时切换武器(AttachToComponent)"
date= "2017-12-19T18:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "AttachToComponent"]
+++

https://github.com/tomlooman/EpicSurvivalGameSeries/blob/4a6ee9a6081529fadbe0f693b2e4e6729d5ec08d/SurvivalGame/Source/SurvivalGame/Private/Items/SWeapon.cpp#L106

EpicSurvivalGameSeries\SurvivalGame\Source\SurvivalGame\Private\Items\SWeapon.cpp

	void ASWeapon::AttachMeshToPawn(EInventorySlot Slot)
	{
		if (MyPawn)
		{
			// Remove and hide
			DetachMeshFromPawn();

			USkeletalMeshComponent* PawnMesh = MyPawn->GetMesh();
			FName AttachPoint = MyPawn->GetInventoryAttachPoint(Slot);
			Mesh->SetHiddenInGame(false);
			Mesh->AttachToComponent(PawnMesh, FAttachmentTransformRules::SnapToTargetNotIncludingScale, AttachPoint);
		}
	}


	void ASWeapon::DetachMeshFromPawn()
	{
		Mesh->DetachFromComponent(FDetachmentTransformRules::KeepWorldTransform);
		Mesh->SetHiddenInGame(true);
	}