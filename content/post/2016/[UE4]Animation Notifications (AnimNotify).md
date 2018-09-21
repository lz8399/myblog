---
title: "[UE4]Animation Notifications (AnimNotify)"
date: "2016-10-09T15:05:02+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

keyword: AnimNotify、Animation Notify、动画的事件通知

Animation Notifications (Notifies)  
https://docs.unrealengine.com/latest/INT/Engine/Animation/Sequences/Notifies/


ue4中动画通知的两种方式（蓝图和C++）  
http://blog.csdn.net/yangxuan0261/article/details/52097917


##### Add Custom Parameters in AnimNotify

Steps:

1. Add Custom C++ AnimNotify Class 

        UCLASS()
        class TOWERDEFENSE_API UAnimNotify_Test : public UAnimNotify
        {
            GENERATED_BODY()
            
        protected:

            virtual void Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation) override;

        protected:

            UPROPERTY(EditAnywhere)
                FString Param;
            
        };
        
        void UAnimNotify_Test::Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation)
        {
            Super::Notify(MeshComp, Animation);

            if (Param == TEXT("AAA"))
            {
                ...
            }
        }

2. Add AnimNotify in Animation asset
{{< figure src="/img/20161009-[UE4]Animation Notifications (AnimNotify)/[UE4]Animation Notifications (Notifies)(动画的事件通知)-01.jpg">}} 

3. Edit Custom Parameters
{{< figure src="/img/20161009-[UE4]Animation Notifications (AnimNotify)/[UE4]Animation Notifications (Notifies)(动画的事件通知)-02.jpg">}}

Note: Add custom parameters in AnimNotifyState is same as AnimNotify.


##### Remove Custom AnimNotify

{{< figure src="/img/20161009-[UE4]Animation Notifications (AnimNotify)/[UE4]Animation Notifications (Notifies)(动画的事件通知)-03.jpg">}} 

{{< figure src="/img/20161009-[UE4]Animation Notifications (AnimNotify)/[UE4]Animation Notifications (Notifies)(动画的事件通知)-04.jpg">}} 

##### Difference Between AnimNotify and AnimNotifyState

AnimNotifyState can set notify time range, and it contains callback function `NotifyBegin`, `NotifyTick`, `NotifyEnd`;  
AnimNotify can only be triggered at the moment, only has callback function `Notify`.


Reference: Rename or delete anim notifys?  
https://answers.unrealengine.com/questions/465629/rename-or-delete-anim-notifys.html