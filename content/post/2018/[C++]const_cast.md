+++
title= "[C++]const_cast"
date= "2018-11-30T14:34:40+08:00"
categories= ["C++"]
tags= ["C++"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-016.jpg"
+++
You are not allowed to `const_cast` variables that are actually `const`. This results in undefined behavior. 

<!--more-->

You are not allowed to `const_cast` variables that are actually `const`. This results in undefined behavior. `const_cast` is used to remove the const-ness from references and pointers that ultimately refer to something that is not `const`.

So, this is allowed:

    int i = 0;
    const int& ref = i;
    const int* ptr = &i;

    const_cast<int&>(ref) = 3;
    *const_cast<int*>(ptr) = 3;
    
It's allowed because `i`, the object being assigned to, is not `const`. The below is not allowed:

    const int i = 0;
    const int& ref = i;
    const int* ptr = &i;

    const_cast<int&>(ref) = 3;
    *const_cast<int*>(ptr) = 3;

because here `i` is `const` and you are modifying it by assigning it a new value. The code will compile, but its behavior is undefined (which can mean anything from "it works just fine" to "the program will crash".)

You should initialize constant data members in the constructor's initializers instead of assigning them in the body of constructors:

    Student(const Student & s) 
        : Person(p.getName(), p.getEmailAddress(), p.getBirthDate()),
          school(0),
          studentNumber(s.studentNumber)
    {
        // ...
    }


Reference: how to use const_cast?  
https://stackoverflow.com/questions/19554841/how-to-use-const-cast

***
`找不到你的时候，特别想把自己也藏到让任何人找不到。`