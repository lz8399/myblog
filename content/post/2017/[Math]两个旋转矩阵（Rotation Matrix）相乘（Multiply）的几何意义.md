+++
title= "[Math]两个旋转矩阵（Rotation Matrix）相乘（Multiply）的几何意义"
date= "2017-02-09T16:48:02+08:00"
categories= ["Math"]
tags= ["UE4", "Math"]
+++


讲之前，先说下如果两个Rotation**相加**的意义，比如：

    FRotator Rot1(0.f, 90.f, 0.f);
    FRotator Rot2(90.f,0.f, 0.f);
    FRotator Result = Rot1 + Rot2;



得到的结果FRotator Result(90.f, 90.f, 0.f)，其意义是：
物体相对空间坐标原点的Rotation为(90.f, 90.f, 0.f)，很好理解。

 

如果两个Rotation**转换为Martix并相乘**，比如：

    FRotator Rot1(0.f, 90.f, 0.f);
    FRotator Rot2(90.f,0.f, 0.f);
    FRotator Result =( FRotationMatrix(Rot1) * FRotationMatrix(Rot2)).Rotator;


得到的结果FRotator Result(0.f, 90.f, 90.f)，其意义是：
`先将物体作Rot1旋转，即：Yaw方向（水平平面）旋转90度，然后再假设该物体相对坐标轴原点的旋转量为(0, 0, 0)，即没有作任何旋转，但实际Rotation相对坐标轴原点为(0, 90, 0)；然后再将物体进行Rot2旋转，即Pitch方向（垂直于(90, 0, 0)方向的平面）侧翻90度，因为侧翻90度前假设物体的Rotation是(0, 0, 0)，所以侧翻时所在的平面不再是Yaw=90的平面（垂直于(0, 90, 0)方向），而是Yaw=0的平面（垂直于(90, 0, 0)方向）。没做相关配图，这段话理解起来有点绕，最好用空间思维想象下，可以用手掌比划。`


#### 实际应用：
比如空间中有两个物体：A和B，现在要将A旋转至与B相同的朝向，目前只知道A的相对世界坐标的Rotation Rw(90.f,0.f, 0.f)、B相对A（将A的Rotation当做(0, 0, 0)）的Rotation Rr(0.f, 90.f, 0.f)，求A旋转后的世界坐标Rotation。  
此时的计算公式就是：

    (FRotationMatrix(Rr) * FRotationMatrix(Rw)).Rotator()


注意：`矩阵相乘时，两个乘数的前后位置不同则计算的结果也不同`，比如上面例子，如果是( FRotationMatrix(Rot2) * FRotationMatrix(Rot1)).Rotator，则结果是Rotation(90, -90, -180)。

***
`风起于青萍之末，浪成于微澜之间。 ----先秦·宋玉 《风赋》`