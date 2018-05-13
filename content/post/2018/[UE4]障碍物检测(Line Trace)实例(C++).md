+++
title= "[UE4]障碍物检测(Line Trace)实例(C++)"
date= "2018-03-02T18:46:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

检测两个坐标点之间是否可见的StaticMesh（障碍物检测）

    FCollisionQueryParams TraceParams(TEXT("TraceActor"), true, this);
    TraceParams.bTraceAsyncScene = true;
    TraceParams.bReturnPhysicalMaterial = false;
    TraceParams.bTraceComplex = false;

    FHitResult Hit(ForceInit);
    GetWorld()->LineTraceSingleByChannel(Hit, SelfLoc, TargetLoc, ECC_Visibility, TraceParams);

    UStaticMeshComponent* MeshComp = Cast<UStaticMeshComponent>(Hit.GetComponent());
    if (MeshComp)
    {
        ...
    }
    
***
`一些普通人也获得了巨大的成功，只是因为他们不知道何时放弃。`