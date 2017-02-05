---
title: "[UE4]TMap使用Struct当作key时需要重载的操作符"
date: "2016-10-23T17:20:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

定义struct：

    struct FMyStruct
    {
        // String which identifies our key
        FString UniqueID;

        // Some state which doesn't affect struct identity
        float SomeFloat;

        explicit FMyStruct(float InFloat)
            : UniqueID (FGuid::NewGuid().ToString())
            , SomeFloat(InFloat)
        {
        }
    };
    
    template <typename ValueType>
    struct TMyStructMapKeyFuncs :
        BaseKeyFuncs<
            TPair<FMyStruct, ValueType>,
            FString
        >
    {
    private:
        typedef BaseKeyFuncs<
            TPair<FMyStruct, ValueType>,
            FString
        > Super;

    public:
        typedef typename Super::ElementInitType ElementInitType;
        typedef typename Super::KeyInitType     KeyInitType;

        static KeyInitType GetSetKey(ElementInitType Element)
        {
            return Element.Key.UniqueID;
        }

        static bool Matches(KeyInitType A, KeyInitType B)
        {
            return A.Compare(B, ESearchCase::CaseSensitive) == 0;
        }

        static uint32 GetKeyHash(KeyInitType Key)
        {
            return FCrc::StrCrc32(*Key);
        }
    };


添加struct元素：

    TMap<
        FMyStruct,
        int32,
        FDefaultSetAllocator,
        TMyStructMapKeyFuncs<int32>
    > MyMapToInt32;

    // Add some elements
    MyMapToInt32.Add(FMyStruct(3.14f), 5);
    MyMapToInt32.Add(FMyStruct(1.23f), 2);

##### 参考文档：

TMap KeyFuncs

https://docs.unrealengine.com/latest/INT/Programming/UnrealArchitecture/TMap/index.html#keyfuncs

TMap with struct

https://forums.unrealengine.com/showthread.php?83995-TMap-with-struct

