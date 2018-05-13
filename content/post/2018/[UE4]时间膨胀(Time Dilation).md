+++
title= "[UE4]时间膨胀(Time Dilation)"
date= "2018-03-02T16:20:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

keywords: UE4 slow down game speed, slow down character motion.

全局时间膨胀

    UGameplayStatics::SetGlobalTimeDilation(GetWorld(), 0.4); 
    
单个对象时间膨胀

    this->CustomTimeDilation = 0.4;

参考：  
Global time dilation and C++ spinning objects  
https://answers.unrealengine.com/questions/473060/global-time-dilation-and-c-spinning-objects-need-h.html

***
`亦舒说，美貌的最高级别是明明很美，却不觉得自己美。那么优秀的最高级别呢？或许是明明非常出色，却不把自己的出色太当回事儿。`