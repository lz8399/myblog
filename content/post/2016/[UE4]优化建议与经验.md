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

7，3种光源的性能消耗从低到高：定向光/平行光(Directional Light) < 点光源(Point Light) < 聚光灯(Spot Light)。这个标准不局限于UE4，其他引擎也是这样。当光源数量在场景中达到一定量级时，3种灯光的性能差距也是数量级上差距。

8，BoxComponent的 Generate Overlap Events 设置为false。如果不需要Overlap事件，那么就将该属性设置设置为false，默认为true。当BoxCompont达到一定量级时，开启Generate Overlap Events的性能消耗时关闭情况下的两倍。

Epic Games工程师分享：如何在移动平台上做UE4的UI优化？  
http://youxiputao.com/articles/11743

##### Dedicated Server优化
1，服务端剥离动画数据  
Project Settings -> Engine -> Animation -> 勾选 Strip Animation Data on Dedicated Server.

2，禁用角色刚体

3，Detach角色身上所有的装饰性组件