+++
title= "[UE4]Lerp函数的计算公式"
date= "2016-11-26T18:17:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Math"]
+++


UnrealMathUnlity.h：

    /** Performs a linear interpolation between two values, Alpha ranges from 0-1 */
    template< class T, class U > 
    static FORCEINLINE_DEBUGGABLE T Lerp( const T& A, const T& B, const U& Alpha )
    {
        return (T)(A + Alpha * (B-A));
    }

    /** Performs a linear interpolation between two values, Alpha ranges from 0-1. Handles full numeric range of T */
    template< class T > 
    static FORCEINLINE_DEBUGGABLE T LerpStable( const T& A, const T& B, double Alpha )
    {
        return (T)((A * (1.0 - Alpha)) + (B * Alpha));
    }

    /** Performs a linear interpolation between two values, Alpha ranges from 0-1. Handles full numeric range of T */
    template< class T >
    static FORCEINLINE_DEBUGGABLE T LerpStable(const T& A, const T& B, float Alpha)
    {
        return (T)((A * (1.0f - Alpha)) + (B * Alpha));
    }

    /** Performs a 2D linear interpolation between four values values, FracX, FracY ranges from 0-1 */
    template< class T, class U > 
    static FORCEINLINE_DEBUGGABLE T BiLerp(const T& P00,const T& P10,const T& P01,const T& P11, const U& FracX, const U& FracY)
    {
        return Lerp(
            Lerp(P00,P10,FracX),
            Lerp(P01,P11,FracX),
            FracY
            );
    }
    
##### 使用实例
先定义两个成员变量：

    float LerpTime = 0.f;
    const float LerpDuration = 2.5f;

再在Tick中计算：

    void Tick(float DeltaSecond)
    {
        if(LerpTime < LerpDuration)
        {
            LerpTime += DeltaSecond;
            
            FVector NewLoc = FMath::Lerp<FVector>(SrcLoc, DistLoc, LerpTime / LerpDuration);
        
            MyCharacter->SetActorLocation(NewLoc);
        }
    }