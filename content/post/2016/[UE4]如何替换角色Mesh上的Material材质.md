+++
title= "[UE4]如何替换角色Mesh上的Material材质"
date= "2016-10-11T2:21:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++


.h (located in pawn header file and assigned in Blueprint editor)

    UPROPERTY(EditAnywhere)
    TArray<UMaterialInterface*> Materials;

.h (located in pawn manager responsible for spawning them)

    TSubclassOf<class AMyPawn> PawnClass;
 
 .cpp
 
    FVector spawnLocation = FVector(0.0f, 0.0f, 0.0f);
    FRotator spawnRotation = FRotator::ZeroRotator;
    AMyPawn* pawn = GetWorld()->SpawnActor<AMyPawn>(PawnClass, spawnLocation, spawnRotation);
    if (pawn != nullptr)
    {
        AMyPawn* defaultPawn = PawnClass.GetDefaultObject();
        int32 materialCount = defaultPawn->Materials.Num();
        int m = FMath::RandRange(0, materialCount - 1);

        const TArray<UActorComponent*>& theComponents = pawn->GetComponents();
        int32 componentCount = theComponents.Num();
        for (int32 x = 0; x < componentCount; x++)
        {
            USkeletalMeshComponent* mesh = Cast<USkeletalMeshComponent>(theComponents[x]);
            if (mesh != nullptr)
            {
                mesh->SetMaterial(0, defaultPawn->Materials[m]);
            }
        }
 