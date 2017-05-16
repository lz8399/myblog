---
title: "[C++]如何将std vector反序"
date: "2016-08-17T15:59:40+08:00"
categories:
- C++
tags:
- STL
---

使用std::reverse函数：

    #include <vector>
    #include <iostream>
    #include <iterator>
    #include <algorithm>
     
    int main()
    {
        std::vector<int> v({1,2,3});
        std::reverse(std::begin(v), std::end(v));
        std::cout << v[0] << v[1] << v[2] << '\n';
     
        int a[] = {4, 5, 6, 7};
        std::reverse(std::begin(a), std::end(a));
        std::cout << a[0] << a[1] << a[2] << a[3] << '\n';
    }