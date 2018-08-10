+++
title= "[UE4][线性代数]物体围绕某个点旋转一定角度"
date= "2016-06-08T18:15:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Math"]
+++

##### 三角函数公式

2D上的点围绕某另一个点旋转：
If you rotate point (px, py) around point (ox, oy) by angle theta you'll get:

    p'x = cos(theta) * (px-ox) - sin(theta) * (py-oy) + ox
    p'y = sin(theta) * (px-ox) + cos(theta) * (py-oy) + oy

this is an easy way to rotate a point in 2D.


***
3D上的点围绕某另一个点旋转  
http://stackoverflow.com/questions/13275719/rotate-a-3d-point-around-another-one  

Try to use vector math. decide in which order you rotate, first along x, then along y perhaps.

If you rotate along z, [z' = z]

    x' = x*cos a - y*sin a;
    y' = x*sin a + y*cos a;  
    The same repeated for y-axis: [y'' = y']

    x'' = x'*cos b - z' * sin b;
    z'' = z'*sin b + x' * cos b;  
    Again rotating along x-axis: [x''' = x'']

    y''' = y'' * cos c - z'' * sin c
    z''' = z'' * sin c + y'' * cos c
And finally the question of rotating around some specific "point":

First subtract the point from the coordinates, then apply the rotations and finally add the point back to the result.

The problem, as far as I see, is a close relative to "gimbal lock". The angle w_ny can't be measured relative to the fixed xyz -coordinate system, but to the coordinate system that is rotated by applying the angle w_nx.

As kakTuZ observed, your code converts point to spherical coordinates. There's nothing inherently wrong with that -- with longitude and latitude one can reach all the places in Earth. And if one doesn't care about tilting the Earth equatorial plane relative to it's trajectory around the Sun, it's ok with me.

The result of not rotating the next reference axis along the first w_ny is that two points that are 1 km a part of each other at equator, move closer each other at the poles and at latitude of 90 degrees, they touch. Even though the apparent purpose is to keep them 1 km apart where ever they are rotated.


##### UE4中的实现方式

    FVector A;
    FVector B;
    FRotator C;

A点绕B点旋转C之后的坐标：

    B+C.RotateVector(A-B)



##### 其他参考
Quaternions and spatial rotation  
https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation

Rotation matrix  
https://en.wikipedia.org/wiki/Rotation_matrix#Basic_rotations