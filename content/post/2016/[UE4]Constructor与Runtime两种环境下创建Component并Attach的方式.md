+++
title= "[UE4]Constructor与Runtime两种环境下创建Component并Attach的方式"
date= "2016-05-29T15:47:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++
	
## Component

MyActor.h：

	UShapeComponent * CollisionMesh;
	
##### Constructor中 Create & Attach
MyActor.cpp：

	CollisionMesh = CreateDefaultSubobject<UBoxComponent>(TEXT("TestCollision"));
	if(CollisionMesh)
	{
		CollisionMesh->SetupAttachment(GetRootComponent());
	}

##### Runtime中（非构造） Create & Attach
MyActor.cpp：

	CollisionMesh = NewObject<UBoxComponent>(this);
	if (CollisionMesh)
	{
		CollisionMesh->RegisterComponent();
		CollisionMesh->AttachToComponent(GetRootComponent(), FAttachmentTransformRules::KeepRelativeTransform);
	}

## Actor
##### Runtime中Actor和Actor之间相互Attach

	Actor1 = GetWorld()->SpawnActor<AMyActor>(AMyActor::StaticClass());
	if(Actor1)
	{
		Actor1->AttachToActor(Actor2, FAttachmentTransformRules::KeepRelativeTransform);
	}

##### Constructor中 Create & Attach
很少情况下需要在构造函数执行Actor之间的相关Attach。

	ConstructorHelpers::FObjectFinder<UMaterial> DecalMaterialAsset(TEXT("Material'/Game/TopDownCPP/Blueprints/M_Cursor_Decal.M_Cursor_Decal'"));
	if (DecalMaterialAsset.Succeeded())
	{
		DecalMaterialAsset.AttachToActor(MyActor, FAttachmentTransformRules::KeepRelativeTransform);
	}


	
{{< alert info >}}
AttachToComponent()为引擎的仅次于UObject的子类`ActorComponent`的函数；
AttachToActor为引擎的仅次于UObject的子类`Actor`的函数。
{{< /alert >}}

{{< alert danger >}}
通过NewObject创建Component之后，执行Register的目的是为了触发OnComponentCreate等回调。不执行Create相关的Initial回调会导致后续的Attach失效。
{{< /alert >}}

注意：Actor::AttachToActor()和Actor::AttachTo()为4.12的新版API，旧版本的工程迁移至4.12后，编译提示警告：  
<font color=red>AActor::AttachRootComponentToActor已废弃，需要使用AttachToActor替换</font>

##### 获取 ActorComponent 所属的 Actor

    AActor* GetOwner() const;
    
GetOwner() 会沿着 ActorComponent 到 RootComponent 之间的从属链一直往上走，找到 RootComponent 并返回 RootComponent 所属的 Actor 对象。
