---
title: "[C++]C++11 template alias和using(模板的模板)"
date: "2017-09-29T18:47:40+08:00"
categories:
- C++
tags:
- C++
---

keywords：alias template、模板别名、模板的模板

如果模版的type(T)不是具体类型，也是一个模板，C++11之前的语法不支持，现在C++11提供了新的语法支持这种场景：using identifier attr(optional) = type-id

示例：

    template <template <typename> class>
    struct X
    {
        X()
        {
            std::cout << "1";
        }
    };

    template <typename>
    struct Y
    {
    };

    template <typename T>
    using Z = Y<T>;

    template <>
    struct X<Y>
    {
        X()
        {
            std::cout << "2";
        }
    };
    
    int main(int argc, char* argv[])
    {
        X<Y> x1;
        X<Z> x2;
    }

运行结果：

    21

Type alias, alias template (since C++11)  
http://en.cppreference.com/w/cpp/language/type_alias

***
`尺之木必有节目，寸之玉必有瑕瓋。---《吕氏春秋》`