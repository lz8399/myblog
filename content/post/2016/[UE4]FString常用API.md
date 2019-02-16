+++
title= "[UE4]FString常用API"
date= "2016-03-01T16:45:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++

将int或float转换为string：

    FString NewString = FString::FromInt(YourInt);     
    FString VeryCleanString = FString::SanitizeFloat(YourFloat);  



将FString转换为 TCHAR*：

    FString str;  
    TCHAR *c1 = *str;  

    TCHAR* c2 = str.GetCharArray().GetData();  


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

    
##### 中文字符的FString 转换 char数组

    FString str(TEXT("笑傲江湖DA"));
    const wchar_t* s1 = *str;

    int LenW = wcslen(s1);
    int LenC = LenW * 2;

    //先转换为 char*, 比如 protobuf 不支持 wchar_t，那么可以将中文转换为char，然后储存在protobuf内部。
    char* buf = new char[LenC + 1]();
    memcpy(buf, s1, LenC);

    //验证char*能否还原为 wchar_t 数组
    wchar_t* buf2 = new wchar_t[LenC/2 + 1]();
    memcpy(buf2, buf, LenC);

    
##### TCHAR*、wchar_t*、char* 转换相关
    
    //char 转换为 TCHAR
    TCHAR* msg = ANSI_TO_TCHAR("dddd");  
    TCHAR* msg2 = UTF8_TO_TCHAR("dddd");  

    
    //TCHAR 转换为 char
    char* Str4 = TCHAR_TO_UTF8(*Str);
    char* Str4 = TCHAR_TO_ANSI(*Str);

    //TCHAR 转换为 wchar_t
    FSting Str;
    wchar_t* Str2 = TCHAR_TO_WCHAR(*Str);
    
    //wchar_t 转换为 TCHAR 
    wchar_t Str5[] = L"sss";
    TCHAR* Str6 = (TCHAR*)Str5;
    
{{< alert danger >}}
如果 char* 字符串有中文，转换为 FString 时，必须使用 ANSI_TO_TCHAR() 或者 UTF8_TO_TCHAR()，例如：FString Text = UTF8_TO_TCHAR("牛鼻"); 。否则会出现乱码。
{{< /alert >}}

##### 4.20 android版本的wchar_t到TCHAR转换问题

问题现象：  
{{< alert danger >}}
4.20之前，wchar_t* 和 TCHAR* 之前直接强转没什么问题，但是4.20版本开始，直接强转在android版本下只会截取字符串的第一个字母，之前的内容都丢失。Windows版本没这个问题。
{{< /alert >}}

解决办法：  
使用`TCHAR_TO_WCHAR`和`WCHAR_TO_TCHAR`转换，而不要直接强制转换。强制转换在Windwos版本下没有问题，android就会出现数据错误。

{{< hl-text red >}}
但是使用 WCHAR_TO_TCHAR 在android版本下编译会有错误：
{{< /hl-text >}}

	UATHelper: Packaging (Android (ASTC)):     UE_4.21/Engine/Source/Runtime/Core/Public/Misc/CString.h(658,9) :  error: no matching function for call to 'Strlen'
	
感觉像是引擎的bug，临时解决办法，自己写 wchar_t 转换 TCHAR 的函数：

	bool UMyStringUtil::WCharToTChar(const wchar_t* Src, TCHAR* Dest, int DestLen)
	{
		bool Ret = true;
		if (!Src)
		{
			Ret = false;
		}
		else
		{
			int SrcLen = wcslen(Src) + 1;

			if (SrcLen == 1)
			{
				Ret = false;
			}
			else
			{
				int MinLen = SrcLen < DestLen ? SrcLen : DestLen;
				for (int i = 0; i < MinLen; i++)
				{
					Dest[i] = Src[i];
				}
			}
		}

		return Ret;
	}

使用示例：

	size_t StrLen = wcslen(MyWcharArray) + 1;
	TCHAR *pData = new TCHAR[StrLen];
	FMemory::Memset(pData, 0, StrLen);
	WCharToTChar(MyWcharArray, pData, StrLen);
	