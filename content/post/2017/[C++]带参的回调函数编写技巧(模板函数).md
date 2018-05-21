---
title: "[C++]带参的回调函数编写技巧(模板函数)"
date: "2017-02-28T16:17:40+08:00"
categories:
- C++
tags:
- C++
---


比如要设置一连串的回调函数来响应键盘的0到9数字键，注册回调函数时无法把数字0到9作为函数参数一起注册，那么有没其他办法？答案肯定是有！具体方式如下：

1，先定义好需要回调的函数，假如：

    void TestCallback(int index);


2，再定义一个模板函数将上面的函数封装：

    template<int index>
    void TestCallback()
    {
        TestCallback(index);
    }

3，最后在注册回调时，将数字作为模板类型来注册：

    CallbackMaster->Bind(&MyClass::TestCallback<9>);
    
***
`不积跬步，无以至千里；不积小流，无以成江海。骐骥一跃，不能十步；驽马十驾，功在不舍。锲而舍之，朽木不折；锲而不舍，金石可镂。——《荀子》`