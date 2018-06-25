+++
title= "[UE4]UFunction-ProcessEvent返回值与输出参数获取"
date= "2018-06-22T12:23:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UFunction", "ProcessEvent", "Invoke"]
+++

如果不需要返回值也不需要输出参数，那么只需调用 `ProcessEvent` ：

    UFunction* Fun = Actor->FindFunction(TEXT("TestFun"));
    if(Fun)
    {
        Actor->ProcessEvent(Fun, Buffer);
    }


获取返回值：

    UFunction* Fun = Actor->FindFunction(TEXT("TestFun"));
    if(Fun)
    {
        FFrame frame = FFrame(Actor, Fun, Buffer, NULL, Fun->Children);
        uint8* ReturnValueAdress = Buffer + Fun->ReturnValueOffset;
        int* intp = (int*)ReturnValueAdress; //hardcoded exemple for a int return
        Fun->Invoke(Actor, frame, intp);
    }
    
获取输出参数：

    if(UFunction* Fun = Actor->FindFunction(TEXT("TestFun")))
    {
        if(uint8* Buffer = (uint8*)FMemory_Alloca(Fun->ParmsSize))
        {
            for (TFieldIterator<UProperty> PropIt(Fun, EFieldIteratorFlags::ExcludeSuper); PropIt; ++PropIt)
            {
                UProperty* Property = *PropIt;

                bool isOut = Property->HasAnyPropertyFlags(CPF_OutParm);
                if (!isOut)
                {
                    continue;
                }

                uint8* outValueAddr = Property->ContainerPtrToValuePtr<uint8>(Buffer);
                float* floatp = (float*)outValueAddr;   //hardcoded example for float
            }
        }
    }
    
{{< alert warning >}}
通过 FindFunction 查找的函数必须添加 UFUNCTION() 宏，否则 FindFunction 返回NULL。
{{< /alert >}}


参考自：https://answers.unrealengine.com/questions/516440/ufunction-invoke.html

***
`对的那条路，往往不是最好走的。`