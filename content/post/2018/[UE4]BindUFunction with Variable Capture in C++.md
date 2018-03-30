+++
title= "[UE4]BindUFunction with Variable Capture in C++"
date= "2018-03-30T18:26:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "BindUFunction", "Variable"]
+++


void UMyClass::FunctionWithVar(const FString& MyVar, TFunction<void(const FString&)> InFunction)
{
    MyLambdaHandle = OnMyDelegate.BindStatic([MyVar](TFunction<void(const FString&)> callback) {callback(MyVar);}, InFunction);
    // TODO: You have to track MyLambdaHandle to be able to unregister it when needed
}

https://answers.unrealengine.com/questions/715835/bindufunction-with-variable-capture-in-c.html

