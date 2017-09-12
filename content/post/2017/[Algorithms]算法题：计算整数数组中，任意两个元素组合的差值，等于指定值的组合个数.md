+++
title= "[Algorithms]算法题：计算整数数组中，任意两个元素组合的差值，等于指定值的组合个数"
date= "2017-09-12T12:19:28+08:00"
categories= ["Algorithms"]
tags= ["Algorithms-Search"]
+++

题目：  
给定一个数组a，再给定一个值k，数组a的任意两个元素组合，他们的差值要求等于k，求出这种组合的对数。比如数组{1, 5, 3, 4, 2}，k=2，那么组合对数等于3，因为符合要求的组合为{1,3}、{4,2}、{5,3}。

代码：

    #include <iostream>
    #include <vector>

    int main(int argc, char* argv[])
    {
        std::vector<int> a;
        a.push_back(1);
        a.push_back(5);
        a.push_back(3);
        a.push_back(4);
        a.push_back(2);

        int k = 2;

        int count = 0;
        std::vector<std::vector<int>> paired_eles(a.size(), std::vector<int>());
        for (size_t i = 0; i < a.size(); i++)
        {
            for (size_t j = i; j < a.size(); j++)
            {
                if (i == j)
                {
                    continue;
                }

                if (abs(a[i] - a[j]) == k)
                {
                    paired_eles[i].push_back(j);
                    count++;
                }
            }
        }

        std::cout << count << std::endl;

        system("pause");
    }

输出结果：

    3
    