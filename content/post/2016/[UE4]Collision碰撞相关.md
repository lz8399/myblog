+++
title= "[UE4]Collision碰撞相关"
date= "2016-10-12T20:15:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "API"]
+++



##### 如何禁用角色的刚体碰撞检测Collision

禁用Actor上所有Component的碰撞：

    MyCharacter->SetActorEnableCollision(false);

设置以后，角色就可以忽视一切障碍物或者刚体来进行移动了，{{< hl-text red >}} 但是这样会导致 AddMovementInput 失效， SetActorLocation 没问题 {{< /hl-text >}}。

禁用指定 Component 的碰撞：

    MyCharacter->GetMesh()->SetCollisionEnabled(ECollisionEnabled::NoCollision);

##### GetOverlappingActors() 注意事项

GetOverlappingActors() 是获取与当前 Collision 相碰撞的 Actor ，如果一个角色身上有两个 CollisionComponent ，且这两个 CollisionComponent 之间有重叠，即使这两个 CollisionComponent没有和其他 Actor碰撞， GetOverlappingActors() 也会返回当前角色 Actor 。
