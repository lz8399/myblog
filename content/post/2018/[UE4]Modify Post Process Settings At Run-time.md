+++
title= "[UE4]Modify Post Process Settings At Run-time"
date= "2018-08-31T14:47:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

Keywords：运行时期间修改后处理设置,  change post process settings when game is running.

##### 运行时修改Post Process 步骤

1，使用 Camera Component 拉出 Set members in PostProcessSettings 节点。  
Get reference to Camera Component and drag out “Set members in PostProcessSettings” node.
{{< figure src="/img/20180831-[UE4]Modify Post Process Settings At Run-time/[UE4]Modify Post Process Settings At Run-time-01.jpg">}}

2，选中  Set members in PostProcessSettings 节点，然后再在 Detail 面板中勾选需要修改的属性。比如我想修改曝光亮度。  
select “Set members in PostProcessSettings” node, then checked properties which want to modify in Detail Panel. e.g. Brightness of Exposure.
{{< figure src="/img/20180831-[UE4]Modify Post Process Settings At Run-time/[UE4]Modify Post Process Settings At Run-time-02.jpg">}}

3，将 Camera 组件的 属性” Post Process Blend Weight” 设置为1，表示完全启用摄像机的 Post Process Settings。0表示完全禁用，0到1的数值表示混合过渡“全完启用”到“完全禁用”之间的渐变效果。  
Set “ Post Process Blend Weight” to 1 in Camera Component, which means fully enable Post Process Settings of Camera. Fully disable Post Process Settings of Camera if set this value to 0, value between 0 and 1 means that using a more gradual blend between fully enabled and fully disabled.
{{< figure src="/img/20180831-[UE4]Modify Post Process Settings At Run-time/[UE4]Modify Post Process Settings At Run-time-03.jpg">}}

4，禁用场景中的Post Process Volume（后处理体积），因为我们使用摄像机组件来接管后处理。  
Disable Post Process Volume in scene, because we would use Post Process Settings of Camera Component.
{{< figure src="/img/20180831-[UE4]Modify Post Process Settings At Run-time/[UE4]Modify Post Process Settings At Run-time-04.jpg">}}

参考实例：游戏启动后，逐渐修改后处理的曝光亮度效果。  
Example: when game start, modify Exposure Brightness of Post Process gradually.
{{< figure src="/img/20180831-[UE4]Modify Post Process Settings At Run-time/[UE4]Modify Post Process Settings At Run-time-05.jpg">}}

##### Post Process Volume 不支持动态修改且不支持代码控制（包括蓝图、C++）
官方给出解释：
因为 Volume 都是使用 BSP BrushComponent 创建的，这会导致很难使用代码去创建 Volume ，官方很难实现代码控制 Volume 。如果要用代码控制，目前只能使用 Camera Component 的 Post Process Settings。

Creating a PostProcessVolume from C++, anyone done that yet?
https://forums.unrealengine.com/development-discussion/c-gameplay-programming/6490-creating-a-postprocessvolume-from-c-anyone-done-that-yet

