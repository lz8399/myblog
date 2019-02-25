+++
title= "[Android NDK]How to support Android 9.0 when building using NDK r12b"
date= "2019-02-22T17:34:02+08:00"
categories= ["Android"]
tags= ["Android"]
keywords= ["UE4", "NDK", "Android"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-011.jpg"
+++

.
<!--more-->
Compilation Error:

	UATHelper: Packaging (Android (ETC1)): UnrealBuildTool: ERROR: D:/NVPACK/android-sdk-windows/tools/android.bat failed with args --silent update lib-project --path JavaLibs/downloader_library --target android-28
	
Reason:  
NDK API Level not matches the SDK API Level.  
e.g. the max NDK API level of r12b is 24, Compilation would be failed if SDK API Level set to 28.

Solution:  

For NDK r12b, the max API Level must be not large than 24.
{{< figure src="/img/20190222-[Android NDK]How to support Android 9.0 when building using NDK r12b/[Android NDK]How to support Android 9.0 when building using NDK r12b-01.jpg">}}
{{< figure src="/img/20190222-[Android NDK]How to support Android 9.0 when building using NDK r12b/[Android NDK]How to support Android 9.0 when building using NDK r12b-02.jpg">}}

***
`生命中曾经有过的所有灿烂，原来终究，都需要用寂寞来偿还。----马尔克斯《百年孤独》`