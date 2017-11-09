+++
title= "[UE4]优化建议与经验"
date= "2016-12-09T19:17:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Performance", "Optimization"]
keywords= ["UE4性能优化","UE4", "Performance", "Optimization"]
+++

keywords：UE4性能优化、Performance Optimization

1，材质尽量用mask，这样可以节省资源。如果用透明和半透明，会非常耗资源。

2，GPUProfile来统计性能消耗的时候，在editor模式下不是很准，因为编辑器的消耗也算进去了，如果要用，最好以Game模式来查看。

3，UE4不支持640X480的分辨率，如果在这个分辨率下运行程序，会导致程序崩溃。

4，如果角色身上有很多Component需要Attach，尽量在使用时Attach，不要一加载就全部attach，否则当场景中角色很多时，会有严重性能问题。

5，面数对UE4来说不敏感，即使在移动端。ipad 4上，50万的三角面，也能够以30fps帧率稳定运行，移动端主要对贴图大小、材质复杂度较为敏感。

6，地形编辑时，使用Instanced Static Meshes。Intancing会增加GPU的开销，但是可以显著降低CPU的开销。注意：Instancing不会减少CPU draw call次数，要减少draw call次数，需要减少材质种类，提供材质复用率。

