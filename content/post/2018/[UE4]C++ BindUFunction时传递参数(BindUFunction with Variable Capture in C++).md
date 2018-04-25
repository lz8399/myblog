+++
title= "[UE4]C++ BindUFunction时传递参数(BindUFunction with Variable Capture in C++)"
date= "2018-03-30T18:26:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "BindUFunction", "BindUObject","Variable"]
+++

keywords：UE4、BindUFunction、BindUObject、Pass Arguments、Variable

示例1：

    void UMyClass::FunctionWithVar(const FString& MyVar, TFunction<void(const FString&)> InFunction)
    {
        MyLambdaHandle = OnMyDelegate.BindStatic([MyVar](TFunction<void(const FString&)> callback) {callback(MyVar);}, InFunction);
        // TODO: You have to track MyLambdaHandle to be able to unregister it when needed
    }

https://answers.unrealengine.com/questions/715835/bindufunction-with-variable-capture-in-c.html


示例2：

使用固定参数绑定

    DECLARE_DELEGATE(RefreshOne);
     
     class MyClass
     {
     public:
         MyClass()
         {
             one.BindRaw(this, &MyClass::MyFunction, (uint8)1);
         }
     
         void MyFunction(uint8 Val)
         {
             // Whatever
         }
     
         void Invoke()
         {
             one.Execute(); // Will call this->MyFunction((uint8)1);
         }
     
     private:
         RefreshOne one;
     };
     
使用动态参数绑定

    DECLARE_DELEGATE_TwoParams(Delegate, const TCHAR*, float);
     
    struct MyClass
    {
        MyClass()
        {
            del.BindRaw(this, &MyClass::MyFunction, (uint8)1, 'x');
        }

        void MyFunction(const TCHAR* a, float b, uint8 c, char d)
        {
            // Whatever
        }

        void Invoke()
        {
            del.Execute(TEXT("Hello"), 3.14f); // Will call this->MyFunction(TEXT("Hello"), 3.14f, (uint8)1, 'x');
        }

        Delegate del;
    };

Bind delegate with one parameter  
https://answers.unrealengine.com/questions/109955/bind-delegate-with-one-parameter.html

### BindRaw、BindUObject、BindUFunction区别

+ BindRaw()：针对非UObject类型的class。
+ BindUObject()：针对UObject类型Class的非UFUNCTION()函数。
+ BindUFunction：针对UObject类型Class的UFUNCTION()函数。
