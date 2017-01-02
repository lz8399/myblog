+++
title= "[UE4]设置MovementMode时的注意事项"
date= "2016-07-17T13:26:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

如果一个Actor被Spawn出来之后，其MovementMode默认状态是Walking，如果此时Spawn的位置在空中，在没有Controller对其Possess的情况下，其静止在空中，当Possess之后，MovementMode会自动变为Falling，如果想让其继续停留在空中(比如飞行类的角色)，此时再手动将其MovementMode设置为Flying。`绝对不能在possess之前设置，否则设置状态会被引擎修改掉。`