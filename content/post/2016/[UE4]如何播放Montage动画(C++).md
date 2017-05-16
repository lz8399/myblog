+++
title= "[UE4]如何播放Montage动画(C++)"
date= "2016-02-18T16:40:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

假设是在Character内执行，其中MontagePtr为Montage指针：

    float DeathAnimDuration = PlayAnimMontage(MontagePtr) / (GetMesh() && GetMesh()->GlobalAnimRateScale > 0 ? GetMesh()->GlobalAnimRateScale : 1);