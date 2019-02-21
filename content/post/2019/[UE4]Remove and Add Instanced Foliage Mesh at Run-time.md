+++
title= "[UE4]Remove and Add Instanced Foliage Mesh at Run-time"
date= "2019-02-18T22:00:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "InstancedFoliageActor", "InstancedStaticMeshComponent"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-013.jpg"
+++

Keywords：InstancedFoliageActor, AInstancedFoliageActor, 
<!--more-->
UInstancedStaticMeshComponent, InstancedStaticMeshComponent, Instanced Foliage, Instanced Static Mesh, Remove and Add at Run-time

##### Add and Remove Instance

1, Use Foliage Painter to create Instanced Foliage Mesh

{{< figure src="/img/20190218-[UE4]Remove and Add Instanced Foliage Mesh at Run-time/[UE4]Remove and Add Instanced Foliage Mesh at Run-time-01.jpg">}}
{{< figure src="/img/20190218-[UE4]Remove and Add Instanced Foliage Mesh at Run-time/[UE4]Remove and Add Instanced Foliage Mesh at Run-time-02.jpg">}}

2, Test code

GameMode:

	UCLASS(minimalapi)
	class ATestProjGameMode : public AGameModeBase
	{
		GENERATED_BODY()

	public:
		ATestProjGameMode();

	protected:

		void BeginPlay() override;

		UFUNCTION(BlueprintCallable)
			void RemoveAllFoliages();

		UFUNCTION(BlueprintCallable)
			void AddAllFoliages();

	private:

		//Instanced Static Mesh Components Array in current Level.
		TArray<UActorComponent*> InstancedStaticMeshCompArray;

		//Each Instanced Static Mesh's Transform. Key: Instanced Static Mesh Component Name, Value:All Transforms in current Instanced Static Mesh Component
		TMap<FString, TArray<FTransform>> TransformMap;
	};


Begin Play

	void ATestProjGameMode::BeginPlay()
	{
		Super::BeginPlay();

		for (TActorIterator<AInstancedFoliageActor> Iter(GetWorld()); Iter; ++Iter)
		{
			if (*Iter)
			{
				//Get the all InstancedStaticMeshComponent in current Level.
				InstancedStaticMeshCompArray = Iter->GetComponentsByClass(UInstancedStaticMeshComponent::StaticClass());

				//Print the name of InstancedStaticMeshComponent
				for (UActorComponent* ActorComp : InstancedStaticMeshCompArray)
				{
					GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Red, ActorComp->GetName());
				}
				break;
			}
		}
	}

{{< figure src="/img/20190218-[UE4]Remove and Add Instanced Foliage Mesh at Run-time/[UE4]Remove and Add Instanced Foliage Mesh at Run-time-03.jpg">}}

Remove all Foliage

	void ATestProjGameMode::RemoveAllFoliage()
	{
		TransformMap.Empty();

		for (UActorComponent* Comp : InstancedStaticMeshCompArray)
		{
			if (UInstancedStaticMeshComponent* InstancedComp = Cast<UInstancedStaticMeshComponent>(Comp))
			{
				GEngine->AddOnScreenDebugMessage(-1, 10.f, FColor::Green, FString::Printf(TEXT("%d"), InstancedComp->GetInstanceCount()));

				TArray<FTransform> TransformArray;

				for (int i = InstancedComp->GetInstanceCount() - 1; i >= 0; i--)
				{
					//Save the transform of current Instance.
					FTransform Out;
					InstancedComp->GetInstanceTransform(i, Out);
					TransformArray.Add(Out);

					//Remove Instance at Run-time.
					InstancedComp->RemoveInstance(i);
				}

				TransformMap.Add(InstancedComp->GetName(), TransformArray);
			}
		}
	}

{{< figure src="/img/20190218-[UE4]Remove and Add Instanced Foliage Mesh at Run-time/[UE4]Remove and Add Instanced Foliage Mesh at Run-time-04.jpg">}}

{{< alert success >}}
Another way to hide Instance: set Scale of Instance to Zero, using `UInstancedStaticMeshComponent::UpdateInstanceTransform(int32 InstanceIndex, const FTransform& NewInstanceTransform)`
{{< /alert >}}

Add all Foliage

	void ATestProjGameMode::AddAllFoliage()
	{
		for (UActorComponent* Comp : InstancedStaticMeshCompArray)
		{
			if (UInstancedStaticMeshComponent* InstancedComp = Cast<UInstancedStaticMeshComponent>(Comp))
			{
				if (TArray<FTransform>* TransformArray = TransformMap.Find(InstancedComp->GetName()))
				{
					for (FTransform& Trans : *TransformArray)
					{
						//Add Instance at Run-time, use the previous Transform.
						InstancedComp->AddInstance(Trans);
					}
				}
				
			}
		}
	}
{{< figure src="/img/20190218-[UE4]Remove and Add Instanced Foliage Mesh at Run-time/[UE4]Remove and Add Instanced Foliage Mesh at Run-time-05.jpg">}}

{{< alert success >}}
These code are applicable to not only Foliage Painter, but also ProceduralFoliageVolume.
{{< /alert >}}

##### How to get StaticMesh and Materials of Instaced Mesh

e.g. code:

	void ATestProjGameMode::BeginPlay()
	{
		Super::BeginPlay();

		for (TActorIterator<AInstancedFoliageActor> Iter(GetWorld()); Iter; ++Iter)
		{
			if (*Iter)
			{
				//Get the all InstancedStaticMeshComponent in current Level.
				TArray<UActorComponent*> InstancedStaticMeshCompArray = Iter->GetComponentsByClass(UInstancedStaticMeshComponent::StaticClass());
				
				for (UActorComponent* ActorComp : InstancedStaticMeshCompArray)
				{
					if (UInstancedStaticMeshComponent* InstancedComp = Cast<UInstancedStaticMeshComponent>(ActorComp))
					{
						UStaticMesh* Mesh = InstancedComp->GetStaticMesh();

						TArray<UMaterialInterface*> Materials = InstancedComp->GetMaterials();
					}
				}
				break;
			}
		}
	}
	
##### How to set Transform of Instaced Mesh

	void ATestProjGameMode::BeginPlay()
	{
		Super::BeginPlay();

		for (TActorIterator<AInstancedFoliageActor> Iter(GetWorld()); Iter; ++Iter)
		{
			if (*Iter)
			{
				//Get the all InstancedStaticMeshComponent in current Level.
				TArray<UActorComponent*> InstancedStaticMeshCompArray = Iter->GetComponentsByClass(UInstancedStaticMeshComponent::StaticClass());
				
				for (UActorComponent* ActorComp : InstancedStaticMeshCompArray)
				{
					if (UInstancedStaticMeshComponent* InstancedComp = Cast<UInstancedStaticMeshComponent>(ActorComp))
					{
						for (int i = InstancedComp->GetInstanceCount() - 1; i >= 0; i--)
						{
							//Set Transform of Instance
							FTransform NewTransform;
							InstancedComp->UpdateInstanceTransform(i, NewTransform);
						}
					}
				}
				break;
			}
		}
	}

##### Reference

Get locations of foliage instances

	for (TActorIterator<AInstancedFoliageActor> ActorItr(GetWorld()); ActorItr; ++ActorItr)
	{
		AInstancedFoliageActor* FoliageMesh = *ActorItr;

		for (auto& MeshPair : FoliageMesh->FoliageMeshes)
		{
			const FFoliageMeshInfo& MeshInfo = *MeshPair.Value;
			UHierarchicalInstancedStaticMeshComponent* MeshComponent = MeshInfo.Component;
			TArray<FInstancedStaticMeshInstanceData> MeshDataArray = MeshComponent->PerInstanceSMData;
			FString MeshName = MeshComponent->GetStaticMesh()->GetName();

			for (auto& MeshMatrix : MeshDataArray)
			{
				FTransform MeshTransform = FTransform(MeshMatrix.Transform);

				UE_LOG(LogTemp, Warning, TEXT("%s, %f, %f, %f, %f, %f, %f, %f, %f, %f,"),
					*MeshName,
					MeshTransform.GetLocation().X,
					MeshTransform.GetLocation().Y,
					MeshTransform.GetLocation().Z,
					MeshTransform.GetRotation().X,
					MeshTransform.GetRotation().Y,
					MeshTransform.GetRotation().Z,
					MeshTransform.GetScale3D().X,
					MeshTransform.GetScale3D().Y, 
					MeshTransform.GetScale3D().Z);
			}
		}
	}

How to get locations of foliage instances?  
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/1474454-how-to-get-locations-of-foliage-instances

***
`真正的强者，不是没有眼泪的人，而是含着眼泪奔跑的人。`
