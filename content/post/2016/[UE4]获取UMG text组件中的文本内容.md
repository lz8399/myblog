---
title: "[UE4]获取UMG text组件中的文本内容"
date: "2016-09-10T00:42:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

直接调用Text属性是获取不到的的：

    FText txt = TxtboxCmdInput->Text;

要调用GetText()函数

    FText txt = TxtboxCmdInput->GetText();
