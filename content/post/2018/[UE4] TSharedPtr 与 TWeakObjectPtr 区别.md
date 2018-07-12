+++
title= "[UE4] TSharedPtr 与 TWeakObjectPtr 区别"
date= "2018-07-04T16:44:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "GarbageCollect", "TSharedPtr", "TWeakObjectPtr"]
+++

UE4 的 TSharedPtr、TWeakObjectPtr 模仿自 C++11 的 shared_ptr 、 weak_ptr 。

##### TSharedPtr
`TSharedPtr` 相当于对象的引用计数器。每当对 TSharedPtr 赋值一次，该 TSharedPtr 引用对象计数加一，当引用计数为0时，则该对象被自动销毁。TSharedPtr 可以防止对象被垃圾回收，等价于 `UPROPERTY()` （前提是 TSharedPtr 成员变量所属的对象没有被销毁，如果被销毁，则 TSharedPtr 成员变量的计数不再有效）。

用法：

     TSharedPtr<MyUObject> ObjPtr = MakeShareable(NewObject<MyUObject>());
     
{{< alert danger >}}
如果两个 TSharedPtr 相互赋值，则会导致对象永不释放，导致内存泄漏。
{{< /alert >}}

{{< alert warning >}}
Uobject不能使用TSharedPtr进行引用计数，如果一个非UObject的类想加入GC，那么必须继承FGCObject类。
{{< /alert >}}

##### TWeakObjectPtr
`TWeakObjectPtr` 保持的对象不能防止被垃圾回收。若引用的对象在其他地方被销毁，则 `TWeakObjectPtr` 内部的指针自动将被置为NULL，TWeakObjectPtr::IsValid()会返回false。`TSharedPtr` 则没有这个作用。

用法：
    
     TWeakObjectPtr<MyUObject> ObjPtr = NewObject<MyUObject>();

参考资料：  

UE4 TSharedPtr和UObject的垃圾回收  
http://www.v5xy.com/?p=808

There's a Huge Difference, One Will Always Crash  
https://answers.unrealengine.com/questions/48818/whats-the-difference-between-using-tweakobjectptr.html

what is a "weak object pointer"?  
https://answers.unrealengine.com/questions/201186/what-is-a-weak-object-pointer.html