+++
title= "[UE4]Why can't I tag a delegate created with DECLARE_EVENT as a UPROPERTY"
date= "2017-12-16T17:21:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "multicast delegate"]
+++

问题：error : Unrecognized type 'MCPlayerBaseAtkAnim' - type must be a UCLASS, USTRUCT or UENUM

解决办法：去掉MULTICAST对象的UPROPERTY宏。如果要用UPROPERTY，请使用 DECLARE_MULTICAST，而不是 MULTICAST。

Why can't I tag a delegate created with DECLARE_EVENT as a UPROPERTY  
https://answers.unrealengine.com/questions/357296/why-cant-i-tag-a-delegate-created-with-declare-eve.html

Creating a multicast delegate
https://www.packtpub.com/mapt/book/game_development/9781785885549/5/ch05lvl1sec69/creating-a-multicast-delegate

***
`枯藤老树昏鸦，`  
`小桥流水人家，`  
`古道西风瘦马。`  
`夕阳西下，`  
`断肠人在天涯。`  
`----马致远《天净沙·秋思》`