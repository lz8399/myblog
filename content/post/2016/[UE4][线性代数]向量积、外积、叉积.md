+++
title= "[UE4][线性代数]向量积、外积、叉积"
date= "2016-07-23T19:19:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++


叉积
http://baike.baidu.com/view/973423.htm

点积
http://baike.baidu.com/view/2744555.htm

UE4的叉积（向量积、外积）函数：

    FVector::CrossProduct()

UE4的点积（数量积、内积）函数：

    FVector::DotProduct()


具体代码示例

    FVector V1(100.f, 0.f, 0.f);
    FVector V2 = FRotator(0.f, 30.f, 0.f).RotateVector(V1);
    FVector V3 = FRotator(0.f, 45.f, 0.f).RotateVector(V1);
    FVector V4 = FRotator(0.f, 60.f, 0.f).RotateVector(V1);

    float d1 = FVector::DotProduct(V2, V3);
    float d2 = FVector::DotProduct(V3, V2);
    float d3 = FVector::DotProduct(V3, V4);
    float d4 = FVector::DotProduct(V2, V4);

其中各个值为：

    V2 = (86.6f, 50.f, 0.f)
    V3 = (70.7f, 70.7f, 0.f)
    V4 = (50.f, 86.6f, 0.f)
    d1 = 9659.25781
    d2 = 9659.25781
    d3 = 9659.25781
    d4 = 8660.25391