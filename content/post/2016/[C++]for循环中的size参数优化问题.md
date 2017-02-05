---
title: "[CPP]for循环中的size参数优化问题"
date: "2016-10-11T22:11:40+08:00"
categories:
- C++
tags:
- STL
---


之前网上一直有这么一条for循环优化建议：
将size提到第一个分号前，这样可以提高循环的效率，例如：

std::vector<int> aaa;
for (size_t i = 0, size = aaa.size(); i < size; i++)
{
	printf("bbb");
}

这个如果是很多年前，应该是有道理的，但是现在的编译器足够聪明，很多看起不够优化的代码，编译器会帮你处理。
以下反编译结果是在VS2015下运行结果，结果是size不前提反而可以节省两次mov指令

size放在第一个分号后：

        for (size_t i = 0; i < aaa.size(); i++)
    00007FF7629E3147  mov         qword ptr [rbp+48h],0  
    00007FF7629E314F  jmp         _20161011+3Ch (07FF7629E315Ch)  
    00007FF7629E3151  mov         rax,qword ptr [rbp+48h]  
    00007FF7629E3155  inc         rax  
    00007FF7629E3158  mov         qword ptr [rbp+48h],rax  
    00007FF7629E315C  lea         rcx,[aaa]  
    00007FF7629E3160  call        std::vector<int,std::allocator<int> >::size (07FF7629E16BDh)  
    00007FF7629E3165  cmp         qword ptr [rbp+48h],rax  
    00007FF7629E3169  jae         _20161011+59h (07FF7629E3179h)  

size提到第一个分号前：

        for (size_t i = 0, size = aaa.size(); i < size; i++)
    00007FF7629E31F7  mov         qword ptr [rbp+48h],0  
    00007FF7629E31FF  lea         rcx,[aaa]  
    00007FF7629E3203  call        std::vector<int,std::allocator<int> >::size (07FF7629E16BDh)  
    00007FF7629E3208  mov         qword ptr [rbp+68h],rax  
    00007FF7629E320C  jmp         _20161011_a+49h (07FF7629E3219h)  
    00007FF7629E320E  mov         rax,qword ptr [rbp+48h]  
    00007FF7629E3212  inc         rax  
    00007FF7629E3215  mov         qword ptr [rbp+48h],rax  
    00007FF7629E3219  mov         rax,qword ptr [rbp+68h]  
    00007FF7629E321D  cmp         qword ptr [rbp+48h],rax  
    00007FF7629E3221  jae         _20161011_a+61h (07FF7629E3231h)  