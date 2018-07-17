+++
title= "[UE4]Construct component using native properties that value be set in editor"
date= "2018-01-04T20:28:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

使用蓝图中编辑的C++属性值来创建Component。  
Construct component using C++ property that value edit in blueprint.

Header：

    UBoxComponent* BoxComp;
    
    UPROPERTY(EditDefaultsOnly, BlueprintReadWrite, Category = AI)
    FVector BoxSize;
    
    void OnConstruction(const FTransform& Transform) override;
    
CPP:

    AMyActor::AMyActor()
    {
        BoxComp = nullptr;
        BoxSize = FVector::ZeroVector;
    }
    
    void AMyActor::OnConstruction(const FTransform& Transform)
    {
        Super::OnConstruction(Transform);
        
        BoxComp = NewObject<UBoxComponent>(this);
        if(BoxComp)
        {
            BoxComp->RegisterComponent();
            BoxComp->AttachToComponent(RootComponent, FAttachmentTransformRules::KeepRelativeTransform);
            BoxComp->SetBoxExtent(BoxSize);
        }
    }

这样，就可以在编辑器中动态调整BoxComponent的大小了。  
Thus, We can modify the size of component in UE4Editor.