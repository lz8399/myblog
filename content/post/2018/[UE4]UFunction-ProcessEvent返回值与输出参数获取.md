+++
title= "[UE4]UFunction-ProcessEvent返回值与输出参数获取"
date= "2018-06-22T12:23:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UFunction", "ProcessEvent", "Invoke"]
+++

获取返回值：

    UFunction* Fun = Actor->FindFunction(TEXT("TestFun"));
    if(Fun)
    {
        Actor->ProcessEvent(Fun, Buffer);
 
        uint8* ReturnValueAdress = Buffer + Fun->ReturnValueOffset;
        int* intp = (int*)ReturnValueAdress; //hardcoded exemple for a int return
    }
    
获取输出参数：

    if(UFunction* Fun = Actor->FindFunction(TEXT("TestFun")))
    {
        if(uint8* Buffer = (uint8*)FMemory_Alloca(Fun->ParmsSize))
        {
            for (TFieldIterator<UProperty> PropIt(theFunction, EFieldIteratorFlags::ExcludeSuper); PropIt; ++PropIt)
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


参考自：https://answers.unrealengine.com/questions/516440/ufunction-invoke.html

***
`对的那条路，往往不是最好走的。`