---
title: "[Android NDK]错误log：ExtMediaPlayer-JNI(22104) env-IsInstanceOf fails"
date: "2016-10-17T15:35:40+08:00"
categories:
- Android
tags:
- NDK
- Error
---

如果你的android app出现以下两种错误log提示，并不影响你的app运行，如果你的app崩溃，可以忽略下面两种log。

    10-17 16:59:29.263: E/ExtMediaPlayer-JNI(22104): env->IsInstanceOf fails
    10-17 16:59:29.263: E/MediaPlayer-JNI(22104): JNIMediaPlayerFactory: bIsQCMediaPlayerPresent 0
    10-17 16:59:29.263: E/ExtMediaPlayer-JNI(22104): env->IsInstanceOf fails
    10-17 16:59:29.263: E/MediaPlayer-JNI(22104): JNIMediaPlayerFactory: bIsQCMediaPlayerPresent 0


    10-18 00:25:40.894: E/MediaPlayer(28634): stop called in state 1
    10-18 00:25:40.894: E/MediaPlayer(28634): error (-38, 0)
    10-18 00:25:40.903: E/MediaPlayer(28634): Error (-38,0)

这两个错误log的具体原因不清楚，第一个貌似和权限相关。
