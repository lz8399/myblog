---
title: "[C++]vector等容器的元素引用问题"
date: "2016-08-10T13:57:40+08:00"
categories:
- C++
tags:
- STL
---


示例代码：

    struct TestStru
    {
        int val;
        TestStru()
        {
            val = -1;
        }
    };



    std::vector<TestStru> TestArr;

    TestStru e1;
    TestArr.push_back(e1);

    TestStru& e = TestArr[0];
    e.val = 999;

    TestStru e2;
    TestArr.push_back(e2);

变量e为数组TestArr内元素的引用，但是当执行`TestArr.push_back(e2);`时，e就失效了。原因是push_back的时候内部容器有扩容，另外vector的默认容量为0。