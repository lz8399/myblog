---
title: "[UE4]用CPP如何动态创建TextRender"
date: "2016-08-15T23:07:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

关键字：Runtime、TextRender、TextRenderActor

![This is an image](/img/20160815-[UE4]用C++如何动态创建TextRender.jpg)

代码：

    #include "Engine/TextRenderActor.h"
    #include "Components/TextRenderComponent.h"

    void ATopDownTestGameMode::BeginPlay()
     {
         Super::BeginPlay();
     
         Text = GetWorld()->SpawnActor<ATextRenderActor>(ATextRenderActor::StaticClass(), FVector(0.f, 100, 170.f), FRotator(90.f, 180.f, 0.f));
         Text->GetTextRender()->SetText(FText::FromString(TEXT("Dynamic Text")));
         Text->GetTextRender()->SetTextRenderColor(FColor::Red);
         Text->SetActorScale3D(FVector(5.f, 5.f, 5.f));
     }
