+++
title= "[UE4]Change Actor‘s Rotation"
date= "2016-09-06T21:26:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

立即修改：

    MyCharacter->SetActorRotation(FRotator(0.f, 180.f, 0.f));

平滑修改：

    void TickFun()
    {
        FVector MyLoc = MyCharacter->GetActorLocation();
        FVector TargetLoc = FVector(100.f, 100.f, 0.f);
        FVector Dir = (TargetLoc - MyLoc);
        Dir.Normalize();
        MyCharacter->SetActorRotation(FMath::Lerp(MyCharacter->GetActorRotation(), Dir.Rotation(), 0.05f));
    }

参考自：https://answers.unrealengine.com/questions/223469/smoothly-rotate-object.html