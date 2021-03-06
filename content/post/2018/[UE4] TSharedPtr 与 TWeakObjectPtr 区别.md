+++
title= "[UE4] TSharedPtr 与 TWeakObjectPtr 区别"
date= "2018-07-04T16:44:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "GarbageCollect", "TSharedPtr", "TWeakObjectPtr"]
+++

UE4 的 TSharedPtr、TWeakObjectPtr 模仿自 C++11 的 shared_ptr 、 weak_ptr 。

### TSharedPtr
`TSharedPtr` 相当于对象的引用计数器。每当对 TSharedPtr 赋值一次，该 TSharedPtr 引用对象计数加一，当引用计数为0时，则该对象被自动销毁。TSharedPtr 可以防止 raw pointer 对象被垃圾回收，。

用法：

     TSharedPtr<TestClass> ObjPtr = MakeShareable(new TestClass());
     
{{< alert danger >}}
如果两个 TSharedPtr 相互赋值，则会导致对象永不释放，导致内存泄漏。
{{< /alert >}}

{{< alert warning >}}
Uobject 不能使用 TSharedPtr 进行引用计数，非UObject才可以；如果一个非UObject的类想加入GC，那么必须继承FGCObject类。
{{< /alert >}}

### TWeakObjectPtr
`TWeakObjectPtr` 保持的对象不能防止被垃圾回收。若引用的对象在其他地方被销毁，则 `TWeakObjectPtr` 内部的指针自动将被置为NULL，TWeakObjectPtr::IsValid()会返回false。`TSharedPtr` 则没有这个作用。

##### Usage
Assignment

	TWeakObjectPtr<AActor> MyWeakActor;
	MyWeakActor = MyActor;
	
Get value

	AActor* Actor = MyWeakActor.Get();
	
or

	if(MyWeakActor.Get())
	{
		ACharacter* Character = Cast<ACharacter>(MyWeakActor);
	}
	
if `MyActor` has been destroyed, `MyWeakActor.Get()` would return `nullptr`

	MyActor->Destroy();
	bool IsValid = MyWeakActor.Get() != nullptr;	//false
	
{{< alert danger >}}
if `MyActor` has been destroyed, `Cast<AMyCharacter>(MyActor)` would cause crash after a while, but `Cast<AMyCharacter>(MyWeakActor)` would not.
{{< /alert >}}

##### Remove in Array

Examples:

	APawn* TestPawn = GetWorld()->SpawnActor<APawn>(MyPawnClass, FVector(100.f, 100.f, 0.f), FRotator::ZeroRotator);
	APawn* MyPawn = GetWorld()->SpawnActor<APawn>(MyPawnClass, FVector(200.f, 200.f, 0.f), FRotator::ZeroRotator);

	TestArray.Add(TWeakObjectPtr<APawn>(TestPawn));
	TestArray.Add(TWeakObjectPtr<APawn>(MyPawn));
	
	int Num = TestArray.Num();	// 2
	
	TWeakObjectPtr<APawn> WeakPtr1(TestPawn);
	TestArray.Remove(WeakPtr1);
	int Num = TestArray.Num();	// 1

	TWeakObjectPtr<APawn> WeakPtr2(TestPawn);
	TestArray.Remove(WeakPtr2);
	int Num2 = TestArray.Num();	// 1
	
### TWeakPtr

Difference between TWeakPtr and TWeakObjectPtr:

{{< alert danger >}}
TWeakObjectPtr is for weak pointers to UObjects, TWeakPtr for pointers to everything else.  
Since UObjects are garbage collected and shared pointers are reference counted, we cannot have the same weak pointer type for all, unfortunately.
{{< /alert >}}
	

Difference between TWeakPtr and TWeakObjectPtr?  
https://answers.unrealengine.com/questions/298868/difference-between-tweakptr-and-tweakobjectptr.html

#### 参考资料

UE4 TSharedPtr和UObject的垃圾回收  
http://www.v5xy.com/?p=808

There's a Huge Difference, One Will Always Crash  
https://answers.unrealengine.com/questions/48818/whats-the-difference-between-using-tweakobjectptr.html

what is a "weak object pointer"?  
https://answers.unrealengine.com/questions/201186/what-is-a-weak-object-pointer.html

***
`已识乾坤大，犹怜草木青。长空送鸟印，留幻与人灵。` ----马一浮《旷怡亭口占》