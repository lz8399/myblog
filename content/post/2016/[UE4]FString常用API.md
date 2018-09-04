+++
title= "[UE4]FString常用API"
date= "2016-03-01T16:45:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

将int或float转换为string：

    FString NewString = FString::FromInt(YourInt);     
    FString VeryCleanString = FString::SanitizeFloat(YourFloat);  



将FString转换为char*：

    FString s;  
    char *c = *s;  



将string转换为int或者float：

    FString TheString = "123.021";    
    int32 MyShinyNewInt = FCString::Atoi(*TheString);  
    float MyShinyNewFloat = FCString::Atof(*TheString);  



字符串切割：

    FString a("1,2,3");  
    TArray<FString> stringArray;  
    a.ParseIntoArray(stringArray, TEXT(","), false);  



字符串截取：

    FString::Left(int count);  
    FString::Right(int count);  



字符串格式化Format：

    FString Path = FString::Printf(TEXT("StaticMesh'/Game/Shapes/ground_shape_%d.ground_shape_%d'"), i);
    
##### 如何获取FString转换后char之后的长度

比如用TCHAR_TO_ANSI()将tchar转换为char之后，char的长度如何计算？
使用FTCHARToANSI::Length()，示例如下：

    FTCHARToANSI Convert(*String);
    Ar->Serialize((ANSICHAR*)Convert, Convert.Length());

参考自：https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/StringHandling/CharacterEncoding/index.html

    
##### 中文字符的FString和wchar_t数组之间的转换

    FString str(TEXT("笑傲江湖DA"));
    const wchar_t* s1 = *str;

    int LenW = wcslen(s1);
    int LenC = LenW * 2;

    char* buf = new char[LenC + 1]();
    memcpy(buf, s1, LenC);

    wchar_t* buf2 = new wchar_t[LenC/2 + 1]();
    memcpy(buf2, buf, LenC);

    
##### wchar_t*、char* 转换相关

    FSting Str;
    wchar_t* Str2 = TCHAR_TO_WCHAR(*Str);

    char* Str3 = TCHAR_TO_UTF8(*Str);
    
    wchar_t Str4[] = L"sss";
    TCHAR* Str5 = UTF8_TO_TCHAR(Str4);
    