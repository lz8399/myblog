+++
title= "[UE4]Trigger Tick of the object inherited from UObject"
date= "2018-12-13T22:24:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Tick", "UObject", "NewObject"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-012.jpg"
+++

### 1st way: FTickableGameObject

<!--more-->

The object inherited from UObject would not trigger Tick when instanced (NewObject<UObject>()), but AActor and the UActorComponent would trigger Tick.

So how to trigger Tick of the object inherited from UObject?  
The answer is: {{< hl-text green >}}inherit FTickableGameObject and UObject at the same.{{< /hl-text >}}

example source

header:

    UCLASS()
    class UCoolDownMgr : public UObject, public FTickableGameObject
    {
        GENERATED_BODY()
    public:
        // Sets default values for this character's properties
        UCoolDownMgr();
        virtual ~UCoolDownMgr();
     
        // Begin FTickableGameObject Interface.
        virtual void Tick(float DeltaTime) override;
        virtual bool IsTickable() const override;
        virtual TStatId GetStatId() const override;
        // End FTickableGameObject Interface.
        
    private:
        
        //Because engine would construct inner object when game load package (before game start), so we need to add a flag to identify which one is construct on game running.
        bool bIsCreateOnRunning = false;
    };
    
cpp:

    UCoolDownMgr::UCoolDownMgr()
    {
        bIsCreateOnRunning = GIsRunning;
    }

    void UCoolDownMgr::Tick(float DeltaTime)
    {
        //Don't invoke Super::Tick(), otherwise would link failed!!!
        //Super::Tick(DeltaTime);
    }
     
    bool UCoolDownMgr::IsTickable() const
    {
        //notify engine to ingore Tick of the object constructed before game running.
        return bIsCreateOnRunning;
    }
    TStatId UCoolDownMgr::GetStatId() const
    {
        return UObject::GetStatID();
    }
    
{{< alert danger >}}
Because engine would construct inner object when game load package (before game start), so we need to add a flag (`bIsCreateOnRunning`) to identify which one is construct on game running.
{{< /alert >}}

Reference:  
https://blog.csdn.net/yangxuan0261/article/details/52093573

### 2nd way: FTickerDelegate

header:

	/** Delegate for callbacks to Tick */
	FTickerDelegate TickDelegate;
	
	/** Handle to various registered delegates */
	FDelegateHandle TickDelegateHandle;
	
cpp:

	TickDelegate = FTickerDelegate::CreateUObject(this, &UMyObject::MyTick);
	TickDelegateHandle = FTicker::GetCoreTicker().AddTicker(TickDelegate);
	
Tick function:

	bool UMyObject::MyTick(float DeltaSeconds)
	{
	
	}
	
***
`生活总是这样，不能叫人处处都满意。但我们还要热情地活下去。人活一生，值得爱的东西很多，不要因为一个不满意，就灰心。`