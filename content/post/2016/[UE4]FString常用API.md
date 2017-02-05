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