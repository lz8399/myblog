+++
title= "[UE4][线性代数]世界坐标转局部坐标(World Space to Local Space)"
date= "2018-04-13T15:59:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Math"]
+++

keywords：UE4、InverseTransformVector、InverseTransformVector、InverseTransformPosition

实例代码：

    //返回摄像机Rotation相对角色Rotation的偏移量Offset
    FRotator ASBaseCharacter::GetAimOffsets() const
    {
        const FVector AimDirWS = GetBaseAimRotation().Vector();
        const FVector AimDirLS = ActorToWorld().InverseTransformVectorNoScale(AimDirWS);
        const FRotator AimRotLS = AimDirLS.Rotation();

        return AimRotLS;
    }
    
    
https://github.com/tomlooman/EpicSurvivalGameSeries/blob/4a6ee9a6081529fadbe0f693b2e4e6729d5ec08d/SurvivalGame/Source/SurvivalGame/Private/Player/SBaseCharacter.cpp#L374
