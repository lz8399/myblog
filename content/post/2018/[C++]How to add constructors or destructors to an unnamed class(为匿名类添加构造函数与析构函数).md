+++
title= "[C++]How to add constructors or destructors to an unnamed class(为匿名类添加构造函数与析构函数)"
date= "2018-06-06T17:44:40+08:00"
categories= ["C++"]
tags= ["C++"]
+++

keywords：匿名类，匿名结构体、构造函数、析构函数、Lambda

为匿名类添加构造函数与析构函数，有两种方式：

+ C++98中在匿名类内部加一个命名类
+ C++11 Lambda语法

##### C++98
C++98中，可以在匿名类内部放一个命名类(named class )，然后再为命名类添加构造和析构函数，当匿名类构造或析构时，就会去调用命名类的构造函数和析构函数。

    #include <iostream>
    #include <cmath>
    int main() {
       struct {
          struct S {
             double a;
             int b;
             S() : a(sqrt(4)), b(42) { std::cout << "constructed" << std::endl; }
             ~S() { std::cout << "destructed" << std::endl; }
          } s;
       } instance1, instance2;
       std::cout << "body" << std::endl;
    }
    
##### C++11 Lambda

    #include <iostream>
    #include <cmath>
    int main() {
       struct {
          double a { sqrt(4) };
          int b { []{
                std::cout << "constructed" << std::endl;
                return 42; }()
                };
       } instance1, instance2;
    }

##### 参考

How to add constructors/destructors to an unnamed class?  
https://stackoverflow.com/questions/21894450/how-to-add-constructors-destructors-to-an-unnamed-class

C++ lambda表达式与函数对象  
https://www.jianshu.com/p/d686ad9de817