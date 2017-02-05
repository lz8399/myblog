---
title: "[CPP]error C2034  type of bit field too small for number of bits"
date: "2016-10-02T13:40:40+08:00"
categories:
- C++
tags:
- STL
---

原文：http://ju.outofmemory.cn/entry/149128

    struct A 
    {
     int x:1;
     int y:2;
     int z:31;
    };
此时是正确的 

但是：

    struct A 
    {
     int x:1;
     int y:2;
     int z:33;
    };

此时就会有编译错误：`error C2034: 'z' : type of bit field too small for number of bits`



原文：http://zhidao.baidu.com/question/60696610.html

struct/class定义中在成员后面加冒号“：1”是什么意思？

这是位域操作的表示方法，也就是说后面加上“：1”的意思是这个成员的大小占所定义类型的1 bit，“：2”占2 bit，依次类推。当然大小不能超过所定义类型包含的总bit数。
一个bytes(字节)是8 bit(bit)。例如你的结构中定义的类型是u_char，一个字节，共8bit，最大就不能超过8。
32位机下，
short是2字节，共16bit，最大就不能超过16.
int是4字节，共32bit，最大就不能超过32.
依次类推。

`这样定义比较省空间`。例如你上面的结构，定义的变量类型是u_char，是一字节类型，即8bit。
fc_subtype占了4bit，fc_type占2bit,fc_protocol_version占2bit，共8bit，正好是一个字节。
其他八个成员,各占1bit，共8bit，正好也是一个字节。
因此你的结构的大小如果用sizeof（struct frame_control）计算，就是2bytes.
