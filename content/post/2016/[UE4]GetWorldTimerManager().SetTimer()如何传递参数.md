---
title: "[UE4]GetWorldTimerManager().SetTimer()如何传递参数"
date: "2016-10-22T17:35:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

回调函数：

    UFUNCTION()
    void MyUsefulFunction(int32 x, float y);


.h

    FTimerDelegate TimerDel;
     
    FTimerHandle TimerHandle;

.cpp

    int32 MyInt = 10;
    float MyFloat = 20.f;

    //Binding the function with specific values
    TimerDel.BindUFunction(this, FName("MyUsefulFunction"), MyInt, MyFloat);
    //Calling MyUsefulFunction after 5 seconds without looping
    GetWorld()->GetTimerManager().SetTimer(TimerHandle, TimerDel, 5.f, false);

参考自：https://answers.unrealengine.com/questions/165678/using-settimer-on-a-function-with-parameters.html