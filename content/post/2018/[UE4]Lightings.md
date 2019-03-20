+++
title= "[UE4]Lightings"
date= "2018-04-27T14:14:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Lightings"]
+++

keywords：UE4、Lighting、灯光

以下问题都是基于4.18，不排除后续新版本变动。

### Lighting Content Examples

https://docs.unrealengine.com/en-us/Resources/ContentExamples/Lighting


### Light Propagation Volumes
Light Propagation Volumes  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/LightPropagationVolumes

Dynamic GI : Getting the Most out of LPV ( Light Propagation Volume )  
https://forums.unrealengine.com/community/community-content-tools-and-tutorials/103572-dynamic-gi-getting-the-most-out-of-lpv-light-propagation-volume

### Lighting Channels
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/LightingChannels

实际应用：  
假设场景中只有一个平行光，且光照强度较大时，那么角色身上接收不到直接光照的部位（比如脖子），会明显发黑，如果增大 SkyBox 光照强度，那么会影响整个场景的亮度。有没办法只增加角色身上的光照亮度？让阴影区域变亮？解决办法是：Lighting Channels。  
解决办法：  
场景中添加两个平行光，A平行光的 Lighting Channels 只开启Channel 0，B平行光只开启Channel 1，然后角色的 Mesh 同时开启 Channel 0 和 Channel 1。


注意事项：

+ Lighting Channels是动态的，意思是：静态光(Static Lights)或者Mobility为Static的Static Mesh Actor不受Lighting Channels影响。要使用Lighting Channels，Static Mesh Actor和Lights的Mobility必须设置为Stationary或者Movable。
+ 材质类型影响：Lighting Channels只影响直接光照(direct lighting)下Opaque类型材质，Translucent或者Masked类型材质没有效果。
+ Lighting Channels对性能开销不大，可以忽略不计。

移动端的Lighting Channels：

+ 4.13版本开始，才支持移动端的Lighting Channel。
+ 移动端多个Directional Light支持不同Lighting Channels。
+ 一个Primitives只受一个Directional Light影响，如果primitves勾选了多个Lighting Channel，那么只会启用第一个。
+ CSM Shadows只会投射到与光源Lighting Channels相同的primitives上。
+ 动态点光源在移动端支持Lighting Channels的所有特性，与桌面级特性相同。

另外：Lighting Channels不支持运行时修改，就是说Lighting Channels在Actor创建时(比如BeginPlay)设置好以后，之后就无法再修改。

### Occlusion Culling 光源距离裁剪
Project Settings -》 Engine -》 Rendering -》 Culling -》 Min Screen Radius for Lights  

Lights view distance  
https://forums.unrealengine.com/unreal-engine/feedback-for-epic/54065-lights-view-distance


### Lighting Related on Mobile

1, `Static` and `Stationary` Spotlight support on Mobile, but `Movable` Spotlight not support on Mobile before v4.22;

2, `Movable` Pointlight support on Mobile always;

3, {{< hl-text red >}} Testing in v4.21: Static and Stationary Point Light not work on Android Vulkan without building lighting.  
Setting up your lighting in SM5, then building lighting, then switch to Android Vulkan, when start game, lighting would works right.{{< /hl-text>}}

### 物体与摄像机距离超过一定范围时，阴影自动消失的问题

这个问题受两个因素影响：

1，DirectionalLight 的属性 `Dynamic Shadow Distance`，如果值小于物体到摄像机的直线距离，则阴影消失。

2，引擎配置参数 `r.Shadow.RadiusThreshold`，表示在屏幕中大小的屏占比 ，该值受 Settings -》 Engine Scalability Settings -》 Shadow 级别控制。

参考：  
https://answers.unrealengine.com/questions/707241/object-shadows-disappearing-too-early.html?sort=oldest

	
### Ambient Occlusion

DFAO can be used with precomputed lighting, but SSAO can not. DFAO can save GPU cost but would memory usage would increase.

##### Screen Space Ambient Occlusion (SSAO) 

Ambient Occlusion  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/AmbientOcclusion

##### Distance Field Ambient Occlusion (DFAO)

How to enable DFAO

1. Start by navigating to the Modes window, then in the Lights section, select and drag a Sky Light into the Level Viewport.
2. With the Sky Light selected, navigate over to its Details panel and set its Mobility to Movable.
3. Project Settings -> Engine -> Rendering -> Default Settings -> check `Ambient Occlusion`  
or  
Place a post process volume into your level, enable `Unbound` in it's properties and then modify `Intensity` of `AO intensity`.  
4. Project Settings -> Engine -> Rendering -> Lighting -> check `Generate Mesh Distance Fields`

Distance Field Ambient Occlusion  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/DistanceFieldAmbientOcclusion

Using Distance Field Ambient Occlusion  
https://docs.unrealengine.com/en-US/Engine/Rendering/LightingAndShadows/MeshDistanceFields/HowTo/DFHT_2

Mesh Distance Fields  
https://docs.unrealengine.com/en-US/Engine/Rendering/LightingAndShadows/MeshDistanceFields#EnablingDistanceFields

### Lighting Issues

Issue 1:  
Point Light intensity is very low event set `Intensity` to large value.  
Solution:  
Remove Point Light and add a new Point Light into scene and setting up it.

Issue 2:  
There're some strange block on lighting maps even building lighting again.  
Solution:  
Build -> Lighting Quality -> Production, then building lighting again. There're some bug in Preview level of Lighting Quality.

##### Lighting Troubleshooting Guide

LightingTroubleshootingGuide  
https://wiki.unrealengine.com/LightingTroubleshootingGuide#Shadow_Seams.2FShading_Differences_with_Indirect_Lighting

### Reference
Lighting Passes  
https://unrealartoptimization.github.io/book/profiling/passes-lighting/

***
`我只担心一件事，我怕我配不上自己所受的苦难。----陀思妥耶夫斯基`
