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

##### C++播放Montage的指定Section

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

***
`人生如逆旅，我亦是行人。----苏轼《临江仙》`