+++
title= "[C++]cannot convert argument 1 from 'const char [5]' to 'std::string &'"
date= "2018-09-16T20:26:40+08:00"
categories= ["C++"]
tags= ["C++"]
+++

Compiling Error:

{{< hl-text red >}}
error C2664: 'void TestFun01(std::string &)': cannot convert argument 1 from 'const char [5]' to 'std::string &'
{{< /hl-text >}}

Solution:

add `const` to `std::string&` which is a parameter of function, like this:

    void TestFun01(const std::string& text)
    {
        std::cout << text;
    }
    
    void TestFun02()
    {
        TestFun01("abcd");
    }

this would produce compiling error:

    void TestFun01(std::string& text)
    {
        std::cout << text;
    }
    
    void TestFun02()
    {
        TestFun01("abcd");
    }