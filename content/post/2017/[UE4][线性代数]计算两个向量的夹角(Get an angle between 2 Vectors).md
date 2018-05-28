+++
title= "[UE4][线性代数]计算两个向量的夹角(Get an angle between 2 Vectors)"
date= "2017-12-17T03:31:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Math"]
+++

示例代码

	float AimAtAngle = FMath::RadiansToDegrees(acosf(FVector::DotProduct(PlayerDirection, MouseDirection)));

	
参考：How to get an angle between 2 Vectors?  
https://answers.unrealengine.com/questions/31058/how-to-get-an-angle-between-2-vectors.html

***
`两情若是久长时，又岂在、朝朝暮暮！----秦观《鹊桥仙》`