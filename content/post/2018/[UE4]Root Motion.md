+++
title= "[UE4]Root Motion"
date= "2018-09-23T21:06:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Root Motion", "Montage"]
+++

##### 蓝图设置方式

Root Motion 设置步骤：

1. 先在 AnimSequence 的`Asset Detail`面板中勾选`EnableRootMotion`和`Force Root Lock`。
2. 然后基于该 AnimSequence 新建一个 AnimMontage。
3. 然后再在 AnimationBluerpint 中设置`Root Motion Mode`为 `Root Motion From Montages Only`（Class Defaults 面板下，不是Class Settings）。

{{< alert warning >}}
如果你没有使用UE4的服务器、或者使用了UE4服务器但是没有对动画启用Replication（服务端通过 NetMulticast 播放动画），设置为`Root Motion from Enerything`没有问题，如果使用了UE4的Replication，且这些动画文件（AnimSequence, Blendspace, AnimMontage, etc.）勾选了`EnableRootMotion`，那么 Root Motion 也会被同步，影响性能。所以官方文档上的建议是使用默认设置，即：`Root Motion Mode`设置为`Root Motion From Montages Only`，只对Montage的Root Motion进行Replication。
{{< /alert >}}

Root Motion  
https://docs.unrealengine.com/en-US/Engine/Animation/RootMotion

##### C++设置方式

UAnimMontage 的两个属性 `bEnableRootMotionTranslation`、`bEnableRootMotionRotation`，任意一个设置为 true 即可。

AnimMontage.cpp 引擎代码：
    
    bool bRootMotionEnabled = bEnableRootMotionTranslation || bEnableRootMotionRotation;

	if (bRootMotionEnabled)
	{
		for (FSlotAnimationTrack& Slot : SlotAnimTracks)
		{
			for (FAnimSegment& Segment : Slot.AnimTrack.AnimSegments)
			{
				if (Segment.AnimReference)
				{
					Segment.AnimReference->EnableRootMotionSettingFromMontage(true, RootMotionRootLock);
				}
			}
		}
	}

***	
`什么是最困难的？与生活讲和。` ──米奇·阿尔博姆（MitchAlbom）《相约星期二》
