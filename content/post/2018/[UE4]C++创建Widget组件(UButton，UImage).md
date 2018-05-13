+++
title= "[UE4]C++创建Widget组件(UButton，UImage)"
date= "2018-03-31T19:03:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "C++ Create Widget "]
+++

示例：

    void UMyUserWidget::NativeConstruct()
    {
        Super::NativeConstruct();
        
        auto MyCanvas = WidgetTree->ConstructWidget<UCanvasPanel>(UCanvasPanel::StaticClass());
        if(MyCanvas)
        {
            auto MyButton = WidgetTree->ConstructWidget<UButton>(UButton::StaticClass());
            MyCanvas->AddChild(MyButton);
            
            WidgetTree->RootWidget = MyCanvas;
        }
    }


##### 其他参考
Create widget in pure C++  
https://answers.unrealengine.com/questions/470481/create-widget-in-pure-c.html?sort=oldest

***
`曾虑多情损梵行，入山又恐别倾城，世间安得双全法，不负如来不负卿。----仓央嘉措`