---
title: "[C++]基础备忘：显式调用构造"
date: "2017-08-24T16:51:40+08:00"
categories:
- C++
tags:
- C++
---

最近两年一直是在UE4的编译器下使用C++，标准C++的一些基础都快忘了。。。

示例代码：

    #include <iostream>

    class CA
    {
    public:
        //两种初始化成员变量的方法
        CA() : ia_(11)
        {
            fa_ = 0.f;
        }

        CA(int val) : ia_(val)
        {
            fa_ = 0.f;
        }

        //要想让子类能够访问，修饰符不可为private
    protected:
        int ia_;

    private:
        float fa_;
    };

    class CB : public CA
    {

    public:
        //显示调用父类的有参构造函数
        CB() : CA(33), ib_(22)
        {
        }

        int ib()
        {
            return ib_;
        }

        int ia()
        {
            return ia_;
        }

    private:

        int ib_;
    };

    int main(int argc, char* argv[])
    {
        CB b;
        std::cout << b.ia() << " " << b.ib() << std::endl;

        return 0;
    }

***
`君子独立不惭于影，独寝不惭于魂。---《晏子春秋》`