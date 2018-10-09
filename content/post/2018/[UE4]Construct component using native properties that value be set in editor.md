+++
title= "[UE4]Construct component using native properties that value be set in editor"
date= "2018-01-04T20:28:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

##### Method 1

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

##### Method 2

overwirte function `PostEditChangeProperty` of AActor:

    virtual void PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) override;

##### Attention
    
1, How to Detect if PostEditChangeProperty is called from Level editor or classDefault/blueprint editor:
    
    UObjectBaseUtility::IsTemplate();
    
Reference:  
https://answers.unrealengine.com/questions/566843/how-to-detect-if-posteditchangeproperty-is-called.html

2, Why Component is not visible in level editor when modify Transform in PostEditChangeProperty() callback?

Solution:  
Invoke `RegisterComponent()` after transform changed.

example

header:

    UPROPERTY(EditAnywhere, Category = ArrowTransform)
        FVector RelativeLoc;
    
	UPROPERTY(EditAnywhere, Category = ArrowTransform)
        FRotator RelativeRot;
    
    UPROPERTY(VisibleAnywhere, BlueprintReadOnly)
		UArrowComponent* TestComponent;
        
cpp:

    void AMyActor::PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent)
    {
        if (TestComponent)
        {
            TestComponent->SetRelativeLocation(RelativeLoc);
            TestComponent->SetRelativeRotation(RelativeRot);
            
            if (!IsTemplate())
            {
                //if not invoke RegisterComponent(), 
                //TestComponent would disappear in level editor when RelativeLoc or RelativeRot changed.
                TestComponent->RegisterComponent();   
            }
        }
    }
    
