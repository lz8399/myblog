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

BindRaw 示例：

    FTimerDelegate TimerDel;
    TimerDel.BindRaw(this, &MyClass::MyFunction);

BindUObject 示例：

    FTimerDelegate TimerDel;
    TimerDel.BindUObject(this, &AMyCharacter::MyUFunction);

BindUFunction 示例：

    TimerDel.BindUFunction(this, FName("TestFun"));
    
### TScriptDelegate 与 DECLARE_DELEGATE 区别

引擎提供了两种用于绑定函数的代理对象：

+ FScriptDelegate
+ FMulticastScriptDelegate

这两种对象只能使用`BindUFunction`一种方式绑定，因为他们使用的是`DECLARE_DYNAMIC_MULTICAST_DELEGATE`，这种代理对象支持转化为stream，可以在网络中传递。  
FTimerDelegate 之所以能有三种方式绑定，是因为它是由`DECLARE_DELEGATE`定义。


### Event 和 Delegate 区别

Delegate 只能绑定一个回调函数，Delegate执行Execute()函数时，只会触发事先绑定的一个函数；Event可以绑定任意个函数，一旦执行Event的Broadcast()函数，所有回调函数按Add顺序依次执行。

Dynamic Multicast Delegate也可以同时绑定多个回调函数，但是其运行效率要比 Event 慢。

### Event 和 Delegate 共同点

回调函数都不能有返回值。

### Dynamic Delegate 与 常规 Delegate 区别

1, Dynamic Delegates 可以被序列化：即他们的注册函数可以通过名称查找获取，代价是比普通Delegate速度慢。
2, 普通Delegate定义参数时，如果使用引用类型，函数执行时传递的实际参数无效，如果要使用引用类型的参数，则要使用Dynamic Delegates。
例如，以TArray的引用类型为例：

    DECLARE_DYNAMIC_DELEGATE_OneParam(FMyDelegate, const TArray<FString>& MyArray);  
    
***
`天上的神明和星辰，人间的艺术与真纯，我们所敬畏和景仰的，莫过于此。`
