+++
title= "[UE4]如何播放Montage动画(C++)"
date= "2016-02-18T16:40:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

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
	
##### C++动态播放Montage（通过AnimSequence创建）
https://dawnarc.com/2017/12/ue4c--%E5%8A%A8%E6%80%81%E5%88%9B%E5%BB%BAmontage%E5%B9%B6%E6%92%AD%E6%94%BE%E5%8A%A8%E7%94%BB/

##### 其他参考：
How can I play animations strictly from C++?  
https://answers.unrealengine.com/questions/292345/how-can-i-play-animations-strictly-from-c.html

