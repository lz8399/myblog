+++
title= "[UE4]Collision碰撞相关"
date= "2016-10-12T20:15:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++



##### 如何禁用角色的刚体碰撞检测Collision

通常的做法是：

    MyCharacter->SetActorEnableCollision(false);

这样设置以后，角色就可以忽视一切障碍物或者刚体来进行移动了。

另外一种方式：

    MyCharacter->GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);
    
这种第二种方式，不会禁用CollisionComponent的碰撞（个人理解，具体未测试）。

##### GetOverlappingActors() 注意事项

GetOverlappingActors() 是获取与当前 Collision 相碰撞的 Actor ，如果一个角色身上有两个 CollisionComponent ，且这两个 CollisionComponent 之间有重叠，即使这两个 CollisionComponent没有和其他 Actor碰撞， GetOverlappingActors() 也会返回当前角色 Actor 。
