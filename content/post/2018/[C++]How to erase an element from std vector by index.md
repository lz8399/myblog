+++
title= "[C++]How to erase an element from std vector by index"
date= "2018-06-29T21:39:40+08:00"
categories= ["C++"]
tags= ["C++", "Erase by index"]
+++

keywords：C++ 用索引删除 std::vector 中的数组元素

To delete a single element, you could do:

    std::vector<int> vec;

    vec.push_back(6);
    vec.push_back(-17);
    vec.push_back(12);

    // Deletes the second element (vec[1])
    vec.erase(vec.begin() + 1);

Or, to delete more than one element at once:

    // Deletes the second through third elements (vec[1], vec[2])
    vec.erase(vec.begin() + 1, vec.begin() + 3);

参考自：How do I erase an element from std::vector<> by index?  
https://stackoverflow.com/questions/875103/how-do-i-erase-an-element-from-stdvector-by-index

***
`无论精神多么独立的人，感情却总是在寻找一种依附，寻找一种归宿。---路遥《平凡的世界》`