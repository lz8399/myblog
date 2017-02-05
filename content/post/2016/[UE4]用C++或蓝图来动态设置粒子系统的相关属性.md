---
title: "[UE4]用CPP或蓝图来动态设置粒子系统的相关属性"
date: "2016-10-05T13:58:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Particle
---


### 蓝图方式

1，我拿StartContent中官方提供的火焰特效来举例，在蓝图脚本中来修改火焰的颜色
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-01.jpg">}} 

 

2，打开粒子编辑界面，这是粒子发射器中设置好的颜色参数
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-02.jpg">}} 

3，修改：Color Over Lif模组 –》 Color Over Life参数 –》Distribution参数 –》 Distribution Vector Particle Parameter
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-03.jpg">}} 

4，为这个参数起一个当前粒子里面的唯一名字。当然你如果希望多个参数共享一个设置，那么参数也可以同名
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-04.jpg">}} 

5，因为这个特效中和颜色相关的发射器有两个，所以我们这两个发射器中的参数名字设置为同名：ParamFireColor
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-05.jpg">}} 

6，设置参数模式为 DPM Direct
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-06.jpg">}} 

{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-07.jpg">}} 

7，然后将粒子拖入场景中进行编辑。当然你可以通过Spawn在运行时动态生成，但是这里为了方便直接场景中放一个静态的
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-08.jpg">}}  

8，添加一个Instance Parameters参数
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-09.jpg">}} 

9，设置参数名为之前定好的ParamFireColor，类型选择Vector Random
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-10.jpg">}} 

10，启动运行程序，然后我们在游戏运行时动态修改。先找到粒子对象
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-11.jpg">}} 

11，然后在属性面板中，编辑之前添加的参数ParamFireColor，这里我们先改为之前的默认数值
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-12.jpg">}} 

{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-13.jpg">}} 

12，这时修改颜色，场景中的火焰也会即时生效了。这些修改的数值不会保存，因为这是即时数据。
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-14.jpg">}} 

{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-15.jpg">}} 
 

补充内容：用蓝图动态生成并设置颜色方式，按下键盘E时生成火焰并将颜色设置为蓝色
{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-16.jpg">}} 

{{< figure src="/img/20161005-[UE4]用C++或蓝图来动态设置粒子系统的相关属性/[UE4]用C++或蓝图来动态设置粒子系统的相关属性-17.jpg">}} 
 
因为这里没有写随机颜色的逻辑，所以看起来很单薄。


### C++方式

C++方式也需要上面蓝图的前面步骤，从第7步开始，后面的步骤都不需要了。
具体代码如下：

    UParticleSystemComponent* PSC = UGameplayStatics::SpawnEmitterAtLocation(GameMode->GetWorld(), EmitterTemplate, Location, FRotator::ZeroRotator, true);

    PSC->SetColorParameter(FName(TEXT("ParamFireColor")), FLinearColor::Red);

    FLinearColor OutColor;
    PSC->GetColorParameter(FName(TEXT("ParamFireColor ")), OutColor);

`注意：要Get参数之前，必须先Set一次，否则无法Get。`




相关参考：
Particle Instance Parameters Tutorial
https://wiki.unrealengine.com/Particle_Instance_Parameters_Tutorial

