+++
title= "[UE4]GPU Visualizer (GPU Profiling) Specification"
date= "2018-12-22T20:05:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "GPU Profiling", "Performance", "Optimization"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-005.jpg"
+++

keywords: Performance, Optimization, PrePass DDM_AllOpaque(Forced by DBuffer)
<!--more-->

### GPU Visualizer arguments specification

##### PrePass DDM_...

Sense

+ Early rendering of depth(Z) from non-translucent meshed.
+ Required by DBuffer decals.
+ May be used by occlusion culling.
+ Engine -> Rendering -> Optimizations -> Early Z-pass.

Cost affected by

+ Triangle count of opaque objects.
+ Depending on Early Z settings: Overdraw and complexity of Masked materials.

##### ShadowDepths

Sense

+ Generation of depth maps for shadow-casting lights.
+ It's like rendering scene's depth from light's point of view.
+ `sg.ShadowQuality 0...4`

Cost affected by

+ Number and range of shadow-casting lights.
+ Number and triangle count of movable shadow-casting objects.
+ Shadow quality settings.
  

### Reference

UE4 Graphics Profiling: All Categories Guide (Rendering Passes)  
https://www.youtube.com/watch?v=C3lumWdwHmA

GPU Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance/GPU

***
`会挽雕弓如满月，西北望，射天狼。----苏轼《江城子·密州出猎》`
