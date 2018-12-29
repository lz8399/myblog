+++
title= "[UE4][UMG]Create Widget Dynamically using C++"
date= "2018-03-31T19:03:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "C++ Create Widget", "UMG", "Dynamic"]
+++

keyworkds：UE4、C++动态创建Widget、Runtime Create Widget

##### 动态创建 CanvasPanel 并在内部动态创建 Button

在空白蓝图中创建一个 CanvasPanel 并在内部创建一个 Button。假设空白UMG蓝图的默认 CanvasPanel 是动态创建，而不是新建UMG蓝图时自带的那个。  
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
    
##### 动态填充 HorizontalBoxSlot

这里假设把 HorizontalBoxSlot 当作一个背包，然后往这个背包中动态添加道具对象。  
示例：

    void UBags::NativeConstruct()
    {
        Super::NativeConstruct();

        //获取UMG蓝图摆放好的 HorizontalBoxSlot
        UHorizontalBox* HorBox = Cast<UHorizontalBox>(GetWidgetFromName(FName("HorizontalBox_62")));
        if (HorBox)
        {
            //加载道具蓝图 class
            if (UClass* MyWidgetClass = LoadClass<UMyItemWidget>(NULL, TEXT("WidgetBlueprint'/Game/UI/ItemBP.ItemBP_C'")))
            {
                for (int i = 0; i < 5; i++)
                {
                    UMyItemWidget* Item = WidgetTree->ConstructWidget<UMyItemWidget>(MyWidgetClass);
                    UPanelSlot* Slot = HorBox->AddChild(Item);
                    if (UHorizontalBoxSlot* HorSlot = Cast<UHorizontalBoxSlot>(Slot))
                    {
                        //设置大小为填充
                        FSlateChildSize Size(ESlateSizeRule::Type::Fill);
                        HorSlot->SetSize(Size);

                        //横向居中对其
                        HorSlot->SetHorizontalAlignment(EHorizontalAlignment::HAlign_Center);
                        
                        //纵向居中对其
                        HorSlot->SetVerticalAlignment(EVerticalAlignment::VAlign_Center);
                    }
                }
            }
        }
    }

##### 动态填充 UniformGridPanel

    void UMyUserWidget::NativeConstruct()
    {
        Super::NativeConstruct();

        //获取UMG蓝图摆放好的 HorizontalBoxSlot
        UUniformGridPanel* UniGrid = Cast<UUniformGridPanel>(GetWidgetFromName(FName("UniformGridPanel_01")));
        if (UniGrid)
        {
            UButton* MyButton = WidgetTree->ConstructWidget<UButton>(UButton::StaticClass());
            if(UUniformGridSlot* Slot = UniGrid->AddChildToUniformGrid(MyButton))
            {
                //设置单元格的纵向和横向位置
                Slot->SetRow(5);
                Slot->SetColumn(5);
            }
        }
    }

##### 批量获取并设置 UniformGridPanel 单元格位置

    TArray<UPanelSlot*> Slots = UniformGridPanel->GetSlots();
	int  index = 0;
	for (UPanelSlot* Slot : Slots)
	{
		UUniformGridSlot * UniSlot = Cast<UUniformGridSlot>(Slot);
		if (UniSlot)
		{
			UniSlot->SetRow(index);
			UniSlot->SetColumn(1);
		}
		index++;
	}
    
##### 运行时期间修改Widget屏幕位置
Modify widget's screen position at run-time:

    void UWidget::SetRenderTranslation(FVector2D Translation)
	
##### NativeConstruct's trigger timing

	if(UMyUserWidget* Widget = WidgetTree->ConstructWidget<UMyUserWidget>(UMyUserWidget::StaticClass()))
	{
		//UMyUserWidget::NativeConstruct() would trigger after be AddChild
		MyCanvasPanel->AddChild(Widget);
	}

{{< alert info >}}
`UMyUserWidget::NativeConstruct()` would trigger after be `AddChild`
{{< /alert >}}

##### 其他参考
Create widget in pure C++  
https://answers.unrealengine.com/questions/470481/create-widget-in-pure-c.html?sort=oldest

***
`曾虑多情损梵行，入山又恐别倾城，世间安得双全法，不负如来不负卿。----仓央嘉措`