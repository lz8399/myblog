+++
title= "[C++]C++11 shared_ptr 与 weak_ptr 区别"
date= "2018-07-06T14:19:40+08:00"
categories= ["C++"]
tags= ["C++"]
+++

##### shared_ptr

语法：

    #include <memory>
    
    shared_ptr<A> x(new A);
    
shared_ptr 相当于 对象引用计数器。每当对 shared_ptr 赋值操作一次，则其引用对象的计数+1。当某对象的引用计数为0时，则该对象自动销毁。

##### weak_ptr

语法：

    #include <memory>
    
    weak_ptr<A> x(new A);

weak_ptr 典型应用是缓存：例如我们在缓存中存放了一个 raw pointer 来指向某个对象，如果这个对象在其他地方被销毁了，那么缓存中的这个 raw pointer 指向的对象不存在。如果我们希望某个对象在其他地方被销毁时，缓存中指向该对象的指针也马上被置为 null，那么就可以使用 weak_ptr。

参考自：  
shared_ptr and weak_ptr differences  
https://stackoverflow.com/questions/4984381/shared-ptr-and-weak-ptr-differences

When is std::weak_ptr useful?  
https://stackoverflow.com/questions/12030650/when-is-stdweak-ptr-useful
