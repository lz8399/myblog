---
title: "[UE4]How can I use UFUNCTION(Exec)"
date: "2017-03-25T14:47:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

UE4提供了自定义命令的操作，类似GM，方便测试。

##### 用法
1. 创建一个继承CheatManager的自定义类，然在GM函数上加上标识：

        UFUNCTION(Exec)
    
2. 在PlayerController的构造函数中设置CheatClass：

        AMyPlayerController::AMyPlayerController(const FObjectInitializer& ObjectInitializer) :
            Super::APlayerController(ObjectInitializer)
        {
            CheatClass = UMyCheatManager::StaticClass();
        }

3. 在命令行（按波浪键，shipping模式下无效）中直接调用该函数了。  
假设函数为：

        UFUNCTION(Exec)
            void TestFun(FString Str);
按下波浪键后，则输入：

        TestFun HelloWorld

##### 注意事项
只有以下类的方法可以支持Exec标签：

+ APawn
+ APlayerController
+ UPlayerInput
+ UCheatManager
+ AGameMode
+ UGameInstance
+ AHUD

##### 参考资料
Using Cheat Manager in Unreal Engine 4  
http://zompi.pl/using-cheat-manager-in-unreal-engine-4/