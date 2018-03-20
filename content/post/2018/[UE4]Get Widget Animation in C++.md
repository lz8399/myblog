+++
title= "Get Widget Animation in C++"
date= "2018-03-20T18:49:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Widget Animation", "C++"]
+++

keywords：C++操作控制UMG动画、Widget Animation

示例代码：

    void UMyMenuWidget::AssignAnimations()
    {
        UProperty* prop = GetClass()->PropertyLink;

        // Run through all properties of this class to find any widget animations
        while( prop != nullptr  )
        {
            // Only interested in object properties
            if( prop->GetClass() == UObjectProperty::StaticClass() )
            {
                UObjectProperty* objectProp = Cast<UObjectProperty>(prop);

                // Only want the properties that are widget animations
                if( objectProp->PropertyClass == UWidgetAnimation::StaticClass() )
                {
                    UObject* object = objectProp->GetObjectPropertyValue_InContainer( this );

                    UWidgetAnimation* widgetAnim = Cast<UWidgetAnimation>(object);

                    if( widgetAnim != nullptr )
                    {
                        // DO SOMETHING TO STORE OFF THE ANIM PTR HERE!
                        // E.g. add to a TArray of some struct that holds info for each anim
                    }
                }
            }

            prop = prop->PropertyLinkNext;
        }
    }
    
参考自：Get Widget Animation in C++  
https://answers.unrealengine.com/questions/427948/get-widget-animation-in-c.html