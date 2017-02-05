---
title: "[UE4][CPP]隐藏物体的时候如何将其所有子对象也隐藏"
date: "2016-10-25T23:25:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords: **SetActorHiddenInGame、Children、Child、Batch**

设置MeshComponent的ToggleVisibility为true，默认为false。这样每当设置当前Actor的visibility的时候，附加在其上的所有child也都会同时显示或隐藏。

    Actor->GetStaticMeshComponent()->ToggleVisibility(true);

完整示例：

    MeshActor->SetActorHiddenInGame(true);
    MeshActor->GetStaticMeshComponent()->ToggleVisibility(true);

注意：
`隐藏子对象只对附加在其上（执行过AttachTo）的子对象有效。另外在编辑器中对某对象右键-》AttachTo或者直接拖拽到某个对象下，这样的子对象也是受ToggleVisibility影响的。`

MeshComponent中类似函数还有ToggleActive()