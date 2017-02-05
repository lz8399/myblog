+++
title= "[UE4]中文字符的FString和wchar_t数组之间的转换"
date= "2016-09-11T02:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API", "String"]
+++

代码：

    FString str(TEXT("笑傲江湖DA"));
    const wchar_t* s1 = *str;

    int LenW = wcslen(s1);
    int LenC = LenW * 2;

    char* buf = new char[LenC + 1]();
    memcpy(buf, s1, LenC);

    wchar_t* buf2 = new wchar_t[LenC/2 + 1]();
    memcpy(buf2, buf, LenC);
