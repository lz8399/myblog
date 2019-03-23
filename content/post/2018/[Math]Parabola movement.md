+++
title= "[Math]Parabola movement"
date= "2018-08-29T11:58:02+08:00"
categories= ["Math"]
tags= ["Math"]
+++

keywords：抛物运动、Parabola、重力加速度、Gravitational Speed 、UE4 implement.

header

    AStaticMeshActor* TestCube = nullptr;

    //throw speed
    UPROPERTY(EditDefaultsOnly)
    FVector StartForce = FVector(100.f, 100.f, 2000.f);

    //gravitational acceleration
    float GravityAcclerator = -980.f;

    //accumulated movtion time
    float AccumulateTime = 0.f;

cpp

    void ATestTPGameMode::StartPlay()
    {
        Super::StartPlay();

        //finding the Actor in scene.
        for (TActorIterator<AStaticMeshActor> Iter(GetWorld()); Iter; ++Iter)
        {
            if (Iter->GetName() == TEXT("Cube_2"))
            {
                TestCube = *Iter;
                break;
            }
        }
    }

    void ATestTPGameMode::Tick(float DeltaSeconds)
    {
        Super::Tick(DeltaSeconds);

        AccumulateTime += DeltaSeconds;

        //calculate gravitational speed in real time.
        float ZSpeed = GravityAcclerator * AccumulateTime;

        //calculate summation speed of gravitational speed and throw speed.
        FVector CurrSpeed = StartForce + FVector(0.f, 0.f, ZSpeed) ;

        //calculate movement distance in real time.
        FVector MoveDist = CurrSpeed * DeltaSeconds;

        //set relative location.
        TestCube->AddActorWorldOffset(MoveDist, true);
    }