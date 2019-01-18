+++
title= "[UE4]LogCompile-error-Circular dependency detected for filename"
date= "2018-11-27T21:57:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-017.jpg"
+++

Circular dependency detected for filename

<!--more-->

Compilation Error：

    LogCompile : error : Circular dependency detected for filename D:\Library Storage\Documents\Unreal Projects\DistantHome\Source\DistantHome\Public\Game\DHGameInfo.h!
    
Solution:  
Don't include headers in header, declare class in header and include headers in cpp.

    class forwardedClass;

    class UsingIt
    {
    public:
        forwardedClass* instance;
    }

or
    
    class UsingIt
    {
    public:
        class forwardedClass* instance;
    }
    
Reference:How do you guys combat circular dependencies in your file heads?  
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/109582-how-do-you-guys-combat-circular-dependencies-in-your-file-heads

***
`在我眼里，钱比对象重要，朋友比对象重要，可你要是对我好，钱我都可以给你，就连我交什么样的朋友都是你说的算。`