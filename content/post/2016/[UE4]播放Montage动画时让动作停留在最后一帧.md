---
title: "[UE4]播放Montage动画时让动作停留在最后一帧"
date: "2016-09-15T03:12:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- API
---

三种方式
##### 方式1：
在想要冻结的那一帧内，将SkeletonComponent的GlobalAnimRateScale属性设置为0。
比如想要角色的骨骼定格在第三帧，那么就在动画播放到第三帧的时候将该属性设置为0。

    ACharacter::GetMesh()->GlobalAnimRateScale = 0.f;

##### 方式2:

    ACharacter::GetMesh()->bNoSkeletonUpdate = true;

##### 方式3：

    ACharacter::GetMesh()->bPauseAnims = true;

`注意：正常播放完AnimSequence时，只要不是设置为循环播放，播放完以后会自动停留在最后一帧。只有播放Montage时才需要设置以上属性。`