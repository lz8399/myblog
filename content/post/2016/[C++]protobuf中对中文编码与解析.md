---
title: "[C++]protobuf中对中文编码与解析"
date: "2016-09-11T02:43:40+08:00"
categories:
- C++
tags:
- Protobuf
---

代码：

    std::string str("笑傲江湖DA");

    int Len = str.size();
    char* data = new char[Len]();
    strcpy(data, str.data());

    HProtocol::test t1;
    t1.set_input_str(data);

    char* buff[1024];
    t1.SerializeToArray(buff, 1024);

    HProtocol::test t2;
    t2.ParseFromArray(buff, t1.ByteSize());

    //最终str3的值依然是str的值
    const char* str3 = t2.input_str().data();