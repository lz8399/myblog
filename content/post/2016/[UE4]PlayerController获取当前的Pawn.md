+++
title= "[UE4]PlayerController获取当前的Pawn"
date= "2016-06-19T10:31:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++


一个Controller（包括AIController）只能同时possess一个Pawn。所以GetPawn()返回的就是当前控制的Pawn：

    APawn* Pawn = PC->GetPawn();