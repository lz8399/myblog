+++
title= "[Algorithms]算法题：多个字母任意组合多个新字符串"
date= "2017-09-03T20:22:28+08:00"
categories= ["Algorithms"]
tags= ["Algorithms-String"]
+++

题目：  
比如一串字符，string s = "abcd"，假设里面的每个字符都不重复，求出这些字符任意组合后，形成的所有的新字符串。忽略掉顺序，比如ac和ca是同一种。
例子：  
abc的3个字符可以组合的情况为：
a
b
c
ab
bc
ac
abc

代码：

    #include <iostream>
    #include <string>
    #include <vector>

    int main(int argc, char* argv[])
    {
        std::string s("abcd");

        std::vector<std::string> vec;
        for (size_t i = 0; i < s.length(); i++)
        {
            std::string s1(1, s.at(i));
            vec.push_back(s1);
            for (size_t j = i + 1; j < s.length(); j++)
            {
                for (size_t k = 0; k < s.length() - j; k++)
                {
                    std::string s2 = s.substr(j, k + 1);
                    std::string new_str = s1 + s2;
                    vec.push_back(new_str);
                }
            }
        }

        for (std::string& str : vec)
        {
            std::cout << str << std::endl;
        }

        system("pause");
    }

输出结果：

    a
    ab
    abc
    abcd
    ac
    acd
    ad
    b
    bc
    bcd
    bd
    c
    cd
    d