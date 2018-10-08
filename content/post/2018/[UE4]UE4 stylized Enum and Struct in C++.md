+++
title= "[UE4]UE4 stylized Enum and Struct in C++"
date= "2018-09-21T18:26:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Assertion", "UENUM", "USTRUCT", "枚举", "结构体"]
+++

##### enum

1, define

    UENUM()
    enum Status
    {
      Stopped     UMETA(DisplayName = "Stopped"),
      Moving      UMETA(DisplayName = "Moving"),
      Attacking   UMETA(DisplayName = "Attacking"),
    };

2, using

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = Status)
    TEnumAsByte<Status> status;
    
##### struct

1, define

    USTRUCT(BlueprintType)
    struct TESTPROJ_API FMyStruct
    {
        GENERATED_USTRUCT_BODY()

        UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Test")
            int32 Test;

        FMyStruct()
        {

        }
    };
    
2, using

    UPROPERTY(EditDefaultsOnly, BlueprintReadOnly)
        FMyStruct Test;

    