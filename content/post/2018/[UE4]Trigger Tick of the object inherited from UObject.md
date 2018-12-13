+++
title= "[UE4]Trigger Tick of the object inherited from UObject"
date= "2018-12-13T22:24:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Tick", "UObject"]
+++

The object inherited from UObject would not trigger Tick when instanced, but AActor and the UActorComponent would trigger Tick.

So how to trigger Tick of the object inherited from UObject?  
The answer is: {{< hl-text green >}}inherit FTickableGameObject and UObject at the same.{{< /hl-text >}}

example:

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
    };

Origin Text:  
https://blog.csdn.net/yangxuan0261/article/details/52093573