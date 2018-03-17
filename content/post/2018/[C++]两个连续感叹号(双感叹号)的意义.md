+++
title= "[C++]两个连续感叹号(双感叹号)的意义"
date= "2018-02-03T21:39:40+08:00"
categories= ["C++"]
tags= ["C++", "Syntax"]
+++

一种获取bool值的技巧，在获取bool值的同时有保证代码有可读性。

比如这种写法，直接将一个指针赋给一个bool值，看上去有点怪，不利于阅读。

    void Test(A* Ptr)
    {
        bool b = Ptr;
        ...
    }

但是加两个感叹号，就可以清楚表明我是要明确获得一个bool。

    void Test(A* Ptr)
    {
        bool b = !!Ptr;
        ...
    }
    
当然用三元运算符? : 也可以，不过要多敲一些字符。

    void Test(A* Ptr)
    {
        bool b = Ptr ? true : false;
        ...
    }
    
三种方式的CPU指令数是完全一样，开销相同。

        bool b = !!Ptr;
    003EA318  cmp         dword ptr [Ptr],0  
    003EA31C  je          Test+6Ah (03EA32Ah)  
    003EA31E  mov         dword ptr [ebp-0E8h],1  
    003EA328  jmp         Test+74h (03EA334h)  
    003EA32A  mov         dword ptr [ebp-0E8h],0  
    003EA334  mov         al,byte ptr [ebp-0E8h]  
    003EA33A  mov         byte ptr [b],al
    