+++
title= "C风格new操作符malloc，如何调用构造函数"
date= "2016-06-04T17:40:02+08:00"
categories= ["C++"]
tags= ["Clang"]
+++

keywords：C++, new, placement new

原文：
http://stackoverflow.com/questions/4956249/using-malloc-instead-of-new-and-calling-the-copy-constructor-when-the-object-is

You'll need to use placement new after getting the raw memory from malloc.

    void* mem = malloc(sizeof(S));
    S* s = new (mem) S(); //this is the so called "placement new"

When you're done with the object you have to make sure to explicitly call its destructor.

    s->~S();
    free(mem);