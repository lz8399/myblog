---
title: "[UE4]如何隐藏Actor"
date: "2016-10-12T20:21:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---


三种方式：

1，`MyActor->bHidden = true;`

2, `MyActor->GetMesh()->SetVisibility(false);`

3，`MyActor->SetActorHiddenInGame(true);`
