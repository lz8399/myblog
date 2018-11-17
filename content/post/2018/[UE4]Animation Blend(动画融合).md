+++
title= "[UE4]Animation Blend(动画融合)"
date= "2018-04-13T11:23:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Animation Blend"]
keywords= ["UE4", "Animation Blend", "Blend Nodes"]
+++

keywords：UE4、Animation Blend Nodes、动画融合实例

各个Blend节点的解释：Blend Nodes  
https://docs.unrealengine.com/en-us/Engine/Animation/NodeReference/Blend


动画融合实例可以参考：  

    EpicSurvivalGameSeries\SurvivalGame\Content\AnimStarterPack\Player_AnimBP

该蓝图中实现逻辑：角色握枪动作跟随摄像机方向动态融合。  
项目地址：https://github.com/tomlooman/EpicSurvivalGameSeries

{{< figure src="/img/20180413-[UE4]Animation Blend(动画融合)/[UE4]Animation Blend(动画融合)-01.jpg">}}

{{< figure src="/img/20180413-[UE4]Animation Blend(动画融合)/[UE4]Animation Blend(动画融合)-02.jpg">}}

{{< figure src="/img/20180413-[UE4]Animation Blend(动画融合)/[UE4]Animation Blend(动画融合)-03.jpg">}}

##### Blend Option

AlphaBlend.h

    UENUM()
    enum class EAlphaBlendOption : uint8
    {
        // Linear interpolation
        Linear = 0,
        // Cubic-in interpolation
        Cubic,
        // Hermite-Cubic
        HermiteCubic,
        // Sinusoidal interpolation
        Sinusoidal,
        // Quadratic in-out interpolation
        QuadraticInOut,
        // Cubic in-out interpolation
        CubicInOut,
        // Quartic in-out interpolation
        QuarticInOut,
        // Quintic in-out interpolation
        QuinticInOut,
        // Circular-in interpolation
        CircularIn,
        // Circular-out interpolation
        CircularOut,
        // Circular in-out interpolation
        CircularInOut,
        // Exponential-in interpolation
        ExpIn,
        // Exponential-Out interpolation
        ExpOut,
        // Exponential in-out interpolation
        ExpInOut,
        // Custom interpolation, will use custom curve inside an FAlphaBlend or linear if none has been set
        Custom,
    };
    
**说明**  
ExpOut：动画速度先减速后加速。  
ExpIn：动画速度加速后减速。  

Animation Blend Modes  
https://docs.unrealengine.com/en-us/Engine/Animation/NonLinearBlends

***
`有作用者器宇定是不凡，有智慧者才情决然不露。----弘一法师`