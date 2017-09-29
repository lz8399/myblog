---
title: "[UE4]HUD中绘制文本(Font字体蓝图使用)"
date: "2017-09-13T23:30:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keywords：UE4、Font、HUD、Canvas

1，先获取需要字体ttf或otf文件。如果是windows系统，打开C:\Windows\Fonts\，然后在Ctrl C和Ctrl V需要的字体文件
{{< figure src="/img/20170913-[UE4]HUD中绘制文本(Font字体蓝图使用)/[UE4]HUD中绘制文本(Font字体蓝图使用)-01.jpg">}}

2，现在内容浏览器中新建一个Font蓝图：鼠标右键 -》 User Interface -》 Font。
{{< figure src="/img/20170913-[UE4]HUD中绘制文本(Font字体蓝图使用)/[UE4]HUD中绘制文本(Font字体蓝图使用)-02.jpg">}}

3，打开Font蓝图，然后在Font Family中指定字体文件(ttf或者otf文件)，然后保存。
{{< figure src="/img/20170913-[UE4]HUD中绘制文本(Font字体蓝图使用)/[UE4]HUD中绘制文本(Font字体蓝图使用)-03.jpg">}}

4，在C++代码钟加载Font蓝图

    #include "UObject/ConstructorHelpers.h"

    UFont* Font;
    ConstructorHelpers::FObjectFinder<UFont> FontObject(TEXT("Font'/Game/TopDownCPP/Blueprints/NewFont.NewFont'"));
    if (FontObject.Object)
    {
        Font = FontObject.Object;
    }

比如在HUD中绘制文本时需要指定字体，此时就可以使用上面加载好的字体

    FCanvasTextItem TextItem(Center2D, FText::FromString(FString(TEXT("测试文字"))), Font, FColor::Red);
    Canvas->DrawItem(TextItem);