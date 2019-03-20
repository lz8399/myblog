+++
title= "[UE4]Animation Montage动画相关"
date= "2016-02-18T16:40:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

##### C++如何播放Montage动画

假设是在Character内执行，其中MontagePtr为Montage指针：

	float DeathAnimDuration = PlayAnimMontage(MontagePtr) / (GetMesh() && GetMesh()->GlobalAnimRateScale > 0 ? GetMesh()->GlobalAnimRateScale : 1);

如果只是播放Animation Sequence，可以使用 PlayAnimation()

	if (USkeletalMeshComponent *Mesh = GetMesh())
	{
		Mesh->PlayAnimation(AnimSequence, false);
	}

{{< alert warning >}}
注意：PlayAnimation可以直接来播放AnimSequence，但是不能混合动作。比如当播放完攻击动作后，无法自动回到空闲状态，但是通过Montage的Slot可以完成自动切换动作。
{{< /alert >}}


其他参考：  
How can I play animations strictly from C++?  
https://answers.unrealengine.com/questions/292345/how-can-i-play-animations-strictly-from-c.html

##### C++动态播放Montage（通过AnimSequence创建）

keywords：UE4, C++, AnimSequence, AnimMontage, Slot, 动态创建, 播放动画

首先要在动画蓝图中添加Slot节点，默认的Slot名字为DefaultSlot。这个名字会在C++代码中使用
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-01.jpg">}}

假设已经获取了要播放的AnimSequence对象指针：AnimSeq

    float AnimLength = 0.f;
    if (USkeletalMeshComponent *Mesh = MyActor->FindComponentByClass<USkeletalMeshComponent>())
    {
        if (UAnimInstance *AnimInst = Mesh->GetAnimInstance())
        {
            if (UAnimMontage* Mtg = AnimInst->PlaySlotAnimationAsDynamicMontage(AnimSeq, TEXT("DefaultSlot"), 0.25f, 0.25f, 1.f, 1))
            {
                AnimLength = Mtg->GetPlayLength();
            }
        }
    }
    
{{< alert info >}}
使用 UAnimInstance::PlaySlotAnimationAsDynamicMontage() 播放Montage时，参数 Animation Sequence 中 Notify 仍然对动态生成的 Montage 有效，即：Montage 也会触发同样的Notify。
{{< /alert >}}

{{< alert danger >}}
使用PlaySlotAnimationAsDynamicMontage()播放Montage时，如果不是循环播放的Montage，播放完毕后一定要执行 UAnimInstance::Montage_Stop() 停掉当前Montage，否则会干扰蓝图动画的逻辑，导致切换其他Montage时无效。
{{< /alert >}}

##### 播放Montage动画时让动作停留在最后一帧

keywords：UE4、Montage、C++、播放速度、播放速率、加速播放、减速播放

三种方式  
方式1：
在想要冻结的那一帧内，将SkeletonComponent的GlobalAnimRateScale属性设置为0。  
比如想要角色的骨骼定格在第三帧，那么就在动画播放到第三帧的时候将该属性设置为0。

    ACharacter::GetMesh()->GlobalAnimRateScale = 0.f;

方式2:

    ACharacter::GetMesh()->bNoSkeletonUpdate = true;

方式3：

    ACharacter::GetMesh()->bPauseAnims = true;

{{< alert warning >}}
注意：正常播放完AnimSequence时，只要不是设置为循环播放，播放完以后会自动停留在最后一帧。只有播放Montage时才需要设置以上属性。
{{< /alert >}}

##### C++播放Montage时指定Section

方式1：  
通过第三个参数 StartSectionName 指定 Section
    
    float ACharacter::PlayAnimMontage(class UAnimMontage* AnimMontage, float InPlayRate = 1.f, FName StartSectionName = NAME_None);

方式2：  
使用 `UAnimInstance::Montage_JumpToSection()` 

    if (USkeletalMeshComponent *Mesh = Character->GetMesh())
    {
        if (UAnimInstance *AnimInst = Mesh->GetAnimInstance())
        {
            Char->PlayAnimMontage(MontagePtr);
            AnimInst->Montage_JumpToSection(FName("step_03"), MontagePtr);
        }
    }
    
{{< alert danger >}}
执行 Montage_JumpToSection 时请确保角色动画的正处于Section所属Montage的播放状态，否则 JumpToSection 无效。
{{< /alert >}}

##### Montage Section切换无效的问题(2018-02-11)

keywords: UE4 Montage Section not working

问题现象：  
SetNextSection在编辑器中运行正常，但是在打包版本中无效。

解决办法：  
将SetNextSection替换为JumpToSection。

参考自：Montage unwanted section switching  
https://answers.unrealengine.com/questions/172537/montage-unwanted-section-switching.html

{{< alert warning >}}
如果Section的时间很短，需要将 Blend In 和 Blend Out 设置为 改小或者设置为 0（默认为0.25），否则 JumpToSection 无效果。
{{< /alert >}}

##### Montage 循环播放(2018-10-26)

如果用动画蓝图控制动画切换，直接用动画状态机去指定 AnimSequence 即可，不需要其他设置，因为动画蓝图会自动根据状态机去循环播放指定的 AnimSequence 。  
如果用C++播放Montage，则需要注意以下细节：

1. 如果是使用现成的Montage资源，需要将Montage设置为循环播放，方式如下：  
打开Montage编辑窗口后，先鼠标单击位置1，然后鼠标单击位置2（都是鼠标左键单击）
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-02.jpg">}}
然后Preview Section 进度条中就多了一个 X ，此时表示Montage为循环播放了
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-03.jpg">}}
之后再执行 `ACharacter::PlayAnimMontage()` 就可以自动循环播放指定Montage了。{{< hl-text green >}}PlayAnimMontage() 只需执行一次即可。{{< /hl-text >}}

2. 如果动态创建Montage并播放，则需要将`LoopCount`设置为足够大，比如 9999。这样当前Montage就会循环播放：

        AnimInstance->PlaySlotAnimationAsDynamicMontage(AnimSeq, TEXT("DefaultSlot"), 0.25f, 0.25f, 1.f, 9999));
        
{{< alert danger >}}
这种方式是否可行：不设置Montage循环播放，而是在Tick中不停检测上一次Montage的累计播放时长，当播完时马上执行下一次播放。答案是不可行！！实际效果是：两次的Montage播放之间会有短暂时间切换到Idle状态动画。
{{< /alert >}}

##### 获取当前正在播放的Montage

	UAnimMontage* UAnimInstance::GetCurrentActiveMontage() const
    
##### 停止Montage播放
如果要停止当前正在播放的Montage，则执行`StopAnimMontage()`：

    void ACharacter::StopAnimMontage(class UAnimMontage* AnimMontage);
    
或者

    void UAnimInstance::Montage_Stop(float InBlendOutTime, const UAnimMontage* Montage = NULL);
    
{{< alert warning >}}
如果希望停止播放Montage时有动画融合效果，记得将Montage的Blend Out Time设置为大于0，比如默认值 0.25 。
{{< /alert >}}

{{< alert success >}}
一旦通过StopAnimMontage停止正在播放的Montage，角色就会恢复到待机动作。
{{< /alert >}}


##### Montage 切换时没有融合的问题

原因：  
Montage 的参数`Blend In`被设置为了0。

解决办法：  
将Montage 的参数`Blend In`（Blend Option -> Blend In -> Blend Time）改成大于0，比如默认值0.25。

##### 设置Montage播放结束和融合结束后的回调函数

    //设置Montage播放完毕后的回调
    void UAnimInstance::Montage_SetEndDelegate(FOnMontageEnded & InOnMontageEnded, UAnimMontage* Montage = NULL);
	
    //设置Montage融合完毕后的回调
	void UAnimInstance::Montage_SetBlendingOutDelegate(FOnMontageBlendingOutStarted & InOnMontageBlendingOut, UAnimMontage* Montage = NULL);

##### 动画状态机切换动画时让动画停留在最后一帧

动画蓝图中的State内部播放动画的节点属性`Loop`修改为`false`：
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-04.jpg">}}
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-05.jpg">}}

如果想让动画停留在最后一帧，另一种方式是在动画的结尾添加Notify事件，在事件中修改动画的播放速率为0。

##### Montage播放完毕后自动停止在最后一帧

将`Enable Auto Blend Out`属性设置为false，这样当Montage播放到结尾时不会自动Blend Out，而是停留在最后一帧直到手动Stop。
{{< figure src="/img/20160218-[UE4]Animation Montage动画相关/[UE4]Animation Montage动画相关-06.jpg">}}
    
***
`人生如逆旅，我亦是行人。----苏轼《临江仙》`