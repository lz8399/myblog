+++
title= "[UE4]Spawn出来的actor固定在空中没有自由落体的问题"
date= "2016-05-28T21:42:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++

spawn出来的actor如果没有给人controller（AIController或者PlayerController），则初始的坐标是哪个位置就会固定在这个位置，即使悬浮在空中也不会自由落体，只要给他possess一个controller就可以自由落体了。