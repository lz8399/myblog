+++
title= "[UE4]C++动态创建Montage并播放动画"
date= "2017-12-25T20:36:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "C++", "AnimSequence", "AnimMontage", "Slot", "动态创建", "播放动画"]
+++

keywords：UE4, C++, AnimSequence, AnimMontage, Slot, 动态创建, 播放动画

首先要在动画蓝图中添加Slot节点，默认的Slot名字为DefaultSlot。这个名字会在C++代码中使用
{{< figure src="/img/20171225-[UE4]C++动态创建Montage并播放动画/[UE4]C++动态创建Montage并播放动画-01.jpg">}}


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

##### C++播放Montage动画（静态Montage资源）
http://www.dawnarc.com/2016/02/ue4%E5%A6%82%E4%BD%95%E6%92%AD%E6%94%BEmontage%E5%8A%A8%E7%94%BBc--/

***
`所有的战争都是内战，因为所有的人类都是同胞。——弗朗索瓦·费奈隆（FrancoisFenelon）`