---
title: "[UE4]用DrawDebugLine绘制矩形"
date: "2016-10-08T01:02:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---


自己实现的用DrawDebugLine绘制矩形的函数：


    /* Draw rectangle use line
        @CenterLoc, location of rectangle center
        @Rot, rotation of rectangle
        @Angle, angle of diagonal
        @DiagonalHalve, half of diagonal lenght.
    */
    void DrawDebugTrangle(const FVector& CenterLoc, const FRotator& Rot, float Angle, float DiagonalHalve)
    {
        FVector Point1 = CenterLoc + (Rot + FRotator(0.f, Angle, 0.f)).Vector() * DiagonalHalve;
        FVector Point2 = CenterLoc + (Rot + FRotator(0.f, 90.f + (90.f - Angle), 0.f)).Vector() * DiagonalHalve;
        FVector Point3 = CenterLoc + (Rot + FRotator(0.f, -90.f - (90.f - Angle), 0.f)).Vector() * DiagonalHalve;
        FVector Point4 = CenterLoc + (Rot + FRotator(0.f, -Angle, 0.f)).Vector() * DiagonalHalve;

        DrawDebugLine(MyGameMode->GetWorld(), Point1, Point2, FColor::Green);
        DrawDebugLine(MyGameMode->GetWorld(), Point2, Point3, FColor::Green);
        DrawDebugLine(MyGameMode->GetWorld(), Point3, Point4, FColor::Green);
        DrawDebugLine(MyGameMode->GetWorld(), Point4, Point1, FColor::Green);
    }
