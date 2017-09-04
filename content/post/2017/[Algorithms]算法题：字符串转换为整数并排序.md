+++
title= "[Algorithms]算法题：字符串转换为整数并排序"
date= "2017-09-03T20:22:28+08:00"
categories= ["Algorithms"]
tags= ["Algorithms-String", "Algorithms-Sorting"]
+++

题目：  
给定一组字符串，字符串中的字符都是数字，比如："343"、"4521"、"3"，将这些字符串转换为整数后并升序排序。

代码：

    #include <iostream>
    #include <string>
    #include <vector>
    #include <math.h>

    int main(int argc, char* argv[])
    {
        std::vector<std::string> StrArr;
        StrArr.push_back(std::string("563435"));
        StrArr.push_back(std::string("234234"));
        StrArr.push_back(std::string("454"));
        StrArr.push_back(std::string("5765"));
        StrArr.push_back(std::string("12"));
        StrArr.push_back(std::string("6"));

        //字符串转数字
        std::vector<int> IntArr;
        for (std::string& str : StrArr)
        {
            size_t len = str.length();
            int val = 0;
            for (size_t i = 0; i < len; i++)
            {
                char c = str.at(i);
                int iv = atoi(&c);
                val += pow(10, (len - 1 - i)) * iv;
            }

            IntArr.push_back(val);
        }

        //冒泡排序。升序
        for (size_t i = 0; i < IntArr.size(); i++)
        {
            int iv = IntArr[i];
            for (size_t j = 1; j < IntArr.size(); j++)
            {
                int jv = IntArr[j];
                int jv_prev = IntArr[j - 1];
                if (jv < jv_prev)
                {
                    IntArr[j] = jv_prev;
                    IntArr[j - 1] = jv;
                }
            }
        }

        for (int v : IntArr)
        {
            std::cout << v << std::endl;
        }

        system("pause");
    }

输出结果：

    6
    12
    454
    5765
    234234
    563435