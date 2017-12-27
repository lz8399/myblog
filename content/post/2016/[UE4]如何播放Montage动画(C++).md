+++
title= "[UE4]如何播放Montage动画(C++)"
date= "2016-02-18T16:40:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4","API"]
+++

假设是在Character内执行，其中MontagePtr为Montage指针：

{{< codeblock "test.cpp" "cpp" "http://underscorejs.org/#compact" "test.cpp" >}}
float DeathAnimDuration = PlayAnimMontage(MontagePtr) / (GetMesh() && GetMesh()->GlobalAnimRateScale > 0 ? GetMesh()->GlobalAnimRateScale : 1);
{{< /codeblock >}}

##### C++动态播放Montage（通过AnimSequence创建）
http://www.dawnarc.com/2017/12/ue4c--%E5%8A%A8%E6%80%81%E5%88%9B%E5%BB%BAmontage%E5%B9%B6%E6%92%AD%E6%94%BE%E5%8A%A8%E7%94%BB/
