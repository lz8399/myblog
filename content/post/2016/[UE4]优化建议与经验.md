+++
title= "[UE4]优化建议与经验"
date= "2016-12-09T19:17:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Performance", "Optimization"]
keywords= ["UE4性能优化", "UE4", "Performance", "Optimization"]
+++

keywords：UE4性能优化、Performance Optimization

内容都是处理项目问题的相关笔记，留给自己做备忘录，也分享出来让别人少走弯路。

##### 零散记录

1. GPUProfile来统计性能消耗的时候，在editor模式下不是很准，因为编辑器的消耗也算进去了，如果要用，最好以Game模式来查看。

2. UE4不支持640X480的分辨率，如果在这个分辨率下运行程序，会导致程序崩溃（4.4版本，不知最新版本是否仍有此问题）。

3. 如果角色身上有很多Component需要Attach，尽量在使用时Attach，不要一加载就全部attach，否则当场景中角色很多时，会有严重性能问题。  
比如：场景中有几百个角色，但不是每个角色都需要摄像机和弹簧臂，那么在构造函数中就不要创建摄像机和弹簧臂组件。

4. 面数对UE4来说不敏感，即使在移动端。ipad 4上，50万的三角面，也能够以30fps帧率稳定运行，移动端主要对贴图大小、材质复杂度较为敏感。

5. C++ 比 蓝图快100到1000倍  
[Test] Blueprint vs C++ Performance vs Nativized BP  
https://www.reddit.com/r/unrealengine/comments/6qtxy3/test_blueprint_vs_c_performance_vs_nativized_bp/

6. 开启`Occlusion Culling` (Project Settings -> Engine -> Rendering -> Occlusion Culling，默认已开启)。如果需要强化遮挡剔除的力度（代价是剔除效果比较突兀）以提升渲染效率，将以下属性值增大：  
Min Screen Radius for Lights  
Min Screen Radius for Early Z Pass  
Min Screen Radius for Cascaded Shadow Maps

##### 灯光优化

1. 3种光源的性能消耗从低到高：  
定向光/平行光(Directional Light) < 点光源(Point Light) < 聚光灯(Spot Light)。  
当光源数量在场景中达到一定量级时，3种灯光的性能差距也是数量级上差距。  
{{< alert info >}}
Point Light 和 Spot Light 的消耗到底谁高谁低，UE4官方文档上貌似没找到明确解释。可能两种灯光在不同使用场景下，消耗对比也不一样。Unity早期官方文档给出了两种灯光在GPU上的消耗说明：  
Point Light: They have an average cost on the graphics processor (though point light shadows are the most expensive).  
Spot Light: They are the most expensive on the graphics processor.  
不考虑显存等其他因素的开销，单考虑GPU消耗，Spot Light 比 Point Light贵。
{{< /alert >}}
Unity早期文档：灯光 Light  
http://www.ceeger.com/Components/class-Light.html

2. 在建构光照贴图时，若场景中没有给予Lightmass Importance Volume，会对整个场景做间接光照的采样，产生Indirect Lighting Cache，这对大型游戏场景是相当的浪费，像是游戏角色到不了的中、远景不需要产生Indirect Lighting Cache，这时候就可以在场景中置入Lightmass Importance Volume，指定特定区域内才会产生Indirect Lighting Cache，节省不少建构光照的时间。

3. 点光源和聚光灯尽量不要开启`Cast Volumetric Shadow`。开启后的性能消耗为不开启的性能消耗三倍。

4. 如果开启体积雾，建议将灯光改成静态光，这样在Build Lighting时会生成预计算的体积雾相关数据，这样可以显著提升体积雾性能。体积雾性能消耗巨大。

5. 如果场景没有静态光 Static Light（全是动态光 Movable Light 或者固定光 Stationary Light），则要禁用 Static Lighting，以节省 Static Lighting 相关的开销（比如 LightMaps和ShadowMaps的相关计算）。禁用方式：Project Settings -> Engine -> Rendering -> Lighting -> disable `Allow Static Lighting`。{{< alert success >}}当全动态灯光为性能瓶颈时，禁用Static Lighting可以提升10帧以上。测试用例：我的某个游戏场景，Lighting是瓶颈之一，`r.ScreenPercentage` 修改为400进行压力测试，关闭 Static Lighting 后帧率提升了20帧。因为没有静态光，禁用后光影效果亦无任何损失。{{< /alert >}}

6. AO性能优化。默认AO是关闭的，在超大型场景中，一般灯光会是性能瓶颈之一，特别是动态光场景下。此时关闭AO可以大幅提高帧率。开启AO后（Project Settings -> Engine -> Rendering -> Default Settings -> `Ambient Occlusion`），引擎默认的AO为SSAO(Screen Space Ambient Occlusion), SSAO无法进行预计算，所以GPU性能开销较大，可以修改为DFAO(Distance Field Ambient Occlusion)以提升性能，因为DFAO可以预计算，代价是增加显存开销。  
DFAO开启方式：  
Distance Field Ambient Occlusion  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/DistanceFieldAmbientOcclusion  
DFAO相关的两个优化选项：  
	+ Compress Mesh Distance Fields: 通过压缩`Distance Fields volume texture`来减少显存占用，代价是当使用Level Streaming时会出现Hitch
	+ Eight Bit Mesh Distance Fields: 将`Distance Fields volume texture`从16位格式压缩为8位格式，代价是AO视觉效果变粗燥。
	

##### 阴影优化

1. 如果使用了非静态的Directional Light（Stationary 或者 Movable），场景中有大量单位时，一定要开启`Dynamic Shadow Distance`（默认为0，表示关闭）。  
测试用例： 500 个 Actor 同屏，摄像机高度4000，Stationary类型的 Directional Light 的属性`Dynamic Shadow Distance StationaryLight`的值要大于摄像机到Actor的直线距离（注意：是到每个Actor的直线距离，所以值尽量要设置的大一些，比5000），否则帧率从200 fps 下降到 100 fps。  
`Dynamic Shadow Distance`开启后能提升性能的原因：  
Dynamic Shadow Distance 表示在多少距离内使用动态阴影，超过这个距离之外Fade成静态阴影，而Fade成静态阴影后就可以提升性能。  
2. 逻辑控制Cast Shadow  
虽然灯光提供了属性`DistanceField Shadow Distance`来控制阴影根据摄像机距离投射，但是这种做法是一刀切。比如：假设性能瓶颈是大量怪物的阴影投射，远处山体和建筑的树木的阴影投射对性能影响很小，此时使用`DistanceField Shadow Distance`就会导致场景的表现效果大打折扣。推荐做法是，程序逻辑上控制：如果是怪物对象，只对离摄像机一定距离内的怪物开启阴影。  
物体投射阴影的开关：

		void UPrimitiveComponent::SetCastShadow(bool NewCastShadow)

##### 材质优化

1. 材质类型的性能，从快到慢：Opaque -> Masked -> Translucent。

2. 若场景中有大量单位，比如500个，那么这些单位一定要做材质LOD，并尽可能多的去掉半透明材质（比如在最后两级直接去掉半透明效果），否则性能消耗呈指数级增长。  

3. 如果GPUVisualizer的`BasePass`耗时较高，那么很大一部分原因是材质复杂度过高。

Performance Guidelines for Artists and Designers  
https://docs.unrealengine.com/latest/INT/Engine/Performance/Guidelines/

#### 植被优化

1. 地形编辑时，使用Instanced Static Meshes。Intancing会增加GPU的开销，但是可以显著降低CPU的开销。注意：Instancing不会减少CPU draw call次数，要减少draw call次数，需要减少材质种类，提高材质复用率。

2. 当Instanced Mesh的数量较多时（比如百万级），执行`RemoveInstance`或者`UpdateInstanceTransform`，帧率会狂泻。  
优化办法：操作Instanced Mesh之前，将`UHierarchicalInstancedStaticMeshComponent::bAutoRebuildTreeOnInstanceChanges`设置为false，然后执行你需要的各种Instanced Mesh操作，操作玩之后，然后将`bAutoRebuildTreeOnInstanceChanges`设置为true，然后执行`BuildTreeIfOutdated(true, false);`，这样可以显著减少因操作百万级Instanced Mesh而导致的性能损失。

3. 如果植被材质消耗成为瓶颈时，宁可增加面数，也不要使用 Translucent 材质，Masked酌情使用。比如一根草的面片，其整个形状全部使用三角面拼出来，而不要用一个三角面再加 Mask 或者 Translucent 材质的方式。

##### 物理与碰撞优化

1. BoxComponent的 Generate Overlap Events 设置为false。如果不需要Overlap事件，那么就将该属性设置设置为false，默认为true。当BoxCompont达到一定量级时，开启Generate Overlap Events的性能消耗是关闭情况下的两倍。

2. 如果不需要物理，将 `Simulate Physics` 设置为false。

3. 如果不需要Hit事件，将 `Simulation Generates Hit Events` 设置为false。

4. 如果场景中物体类型（WorldStatic、WorldDynamic、Pawn等）很多，且每种数量也很多，则Collision 的 Object Response 通道设置的越少越好，把可以设置为 Ignore 的通道都设置为 Ignore 。如果场景中的物体类型比较单一，即使这种类型的物体在场景中有数百个，Object Response 即使都设置为Block 或者 Overlap，对性能也没有影响。

5. 如果是大型RTS游戏，场景有海量单位时（比如星际2中大规模的虫族小狗），能不用UE4的 Collision 就不要用 Collision，否则帧数狂泻。  
建议自己实现一个简易的自定义Collision，比如球形Collision，然后计算该 Collision 与单位之间的直线距离，来判断是否是否发生了碰撞，并且降低检测间隔，比如 0.1秒一次。

##### 动画优化
1. 打开角色蓝图 -》 MeshComponent -》 Detail 面板中的 Optimization 类别下 -》 勾选 `Enable Update Rate Optimizations`。

2. 只对渲染的 SkinnedMesh执行 Tick 和 RefreshBoneTransforms

        USkinnedMeshComponent::MeshComponentUpdateFlag = OnlyTickPoseWhenRendered;
        
    默认是`AlwaysTickPoseAndRefreshBones`，表示不管是否被渲染（在可见区域内），都执行 Tick 和 RefreshBoneTransforms。  
    旧版本中`MeshComponentUpdateFlag`叫做`SkinnedMeshUpdateFlag`。  
	{{< alert warning >}} 如果关闭动画Tick，和Tick相关的逻辑就会失效，比如`Transform (Modify) Bone`。{{< /alert >}}
	
3. 动画蓝图的逻辑尽量直接访问成员变量，引擎默认开启了优化选项：动画蓝图中的成员变量在编译时会被复制到Native Code中，从而避免在运行时进入蓝图虚拟机（Blueprint Virtual Machine）执行蓝图代码，因为蓝图VM运行效率低。  
默认会被编译优化的参数类型包括：  
member variables;  
negated boolean member variables;  
members of a nested structure;  
具体说明见官方文档：  
Animation Optimization  
https://docs.unrealengine.com/en-us/Engine/Animation/Optimization  
Animation Fast Path Optimization  
https://docs.unrealengine.com/en-us/Engine/Animation/Optimization/FastPath

##### UI优化

1. 能用HUD解决的就不要用UMG，等到需要显示时才创建Widget对象，不显示时则销毁，UMG对象较多时性能消耗巨大。  
比如场景内有一千个单位，每个单位上都创建有WidgetComponent，即使这些WidgetComponent没有显示任何东西，也会产生巨大的GPU开销。

Epic Games工程师分享：如何在移动平台上做UE4的UI优化？  
http://youxiputao.com/articles/11743

##### 位移优化

1. 海量Pawn（比如500个）单位移动，如果是在 Tick 中使用 AddMovementInput 移动，帧率直接下降一半（比如从90帧下降到40多帧）。对于无法移动的单位，最好停止执行 AddMovementInput() ，以提升性能。

##### 特效优化
1. 尽量不要使用 Volume domain，使用后会显著增加GPU开销。可以通过 `profilegpu` 检测 Volume 开销。

##### AI优化

1. 如果角色不需要 Controller ，就不要给它 Spawn Controller。如果一个角色长时间停止，则先给他`Unpossesed()` ，等到可移动时再`PossessedBy()`。  
测试：500个角色，AI Controller Class 设置为：null、 AIController、PlayerController 的帧数分别为 120 fps、 100 fps、75 fps。

##### Dedicated Server优化
1. 服务端cook时剥离动画数据  
Project Settings -> Engine -> Animation -> 勾选 Strip Animation Data on Dedicated Server.  
如果在动画中添加了触发修改数据的 Notify Event，勾选此选项会有问题。请确保动画中挂载的 Notify 只是表现相关，不涉及游戏逻辑。

2. Server模式下禁用角色物理模拟  
`FBodyInstance->bSimulatePhysics` 设置为false。默认为false。  
`SkeletalMeshComponent::bEnablePhysicsOnDedicatedServer` 设置为 false ， 默认为 true 。但这样会导致物理验算以客户端为准，有被外挂hack的风险。bEnablePhysicsOnDedicatedServer 在 run-time 修改不生效。

3. Server模式下禁用 Collision  
`UPrimitiveComponent->bGenerateOverlapEvents` 设置为false，角色蓝图中的 CollisionComponent 默认为true。

4. Server模式下Detach角色身上所有的装饰性组件

##### 参考资料

Performance and Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance

通过优化在UE4中实现良好性能和高质量视觉效果  
http://gad.qq.com/program/translateview/7160166

CPU Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance/CPU

GPU Profiling  
https://docs.unrealengine.com/en-us/Engine/Performance/GPU

Unreal Engine 4 Optimization Tutorial, Part 1-4  
https://software.intel.com/en-us/articles/unreal-engine-4-optimization-tutorial-part-1  
https://software.intel.com/en-us/articles/unreal-engine-4-optimization-tutorial-part-2  
https://software.intel.com/en-us/articles/unreal-engine-4-optimization-tutorial-part-3  
https://software.intel.com/en-us/articles/unreal-engine-4-optimization-tutorial-part-4

Optimizing and Profiling Games with Unreal Engine 4  
http://vincentloignon.com/blog/optimizing-and-profiling-games-with-unreal-engine-4/

Dynamic Lighting Portal System (Performance Booster)  
https://www.unrealengine.com/marketplace/dynamic-lighting-portal-system-performance-booster

Performance Optimization: Shadows Triggering Zones  
https://www.unrealengine.com/marketplace/performance-optimization-shadows-triggering-zones
