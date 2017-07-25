---
title: "[UE4]动画蓝图的编辑全流程(Animation Blueprint)"
date: "2017-06-17T21:45:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Keyword: UE4、Animation Blueprin、Montage Slot、Character Blueprint

不知从从哪个版本开始，动画蓝图的制作和老版本之间的差距有点大了，这里做下笔记，以备不时之需。。  
UE4版本：4.16  

假设已经将模型和动作导入工程了，这里使用官方模板项目的动作作为例子讲解，只演示待机、跑步的控制逻辑，跳跃的可以看项目模板的动画蓝图。

1，准备好动作和模型
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-01.jpg">}}

2，新建一个Blend Space 1D
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-02.jpg">}}

然后在跳出的菜单中选择骨骼
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-03.jpg">}}

3，打开Blend Space 1D蓝图，分别将待机、行走、跑步三个动作拖拽到下方面板钟
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-04.jpg">}}

修改驱动属性名为Speed，默认为None，这个属性名为是后面编辑动画蓝图使用的属性名。
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-05.jpg">}}

最终效果：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-06.jpg">}}

4，将`TargetWeightInterpolationSpeedPerSec`修改为5.0，修改这个值的原因是为了让角色移动时的静止和移动的过度更加自然
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-07.jpg">}}

5，新建一个动画蓝图（Animation Blueprin）:
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-08.jpg">}}

在弹出的菜单钟选择父类和骨骼，父类为：AnimInstance；骨骼就是当前模型的骨骼
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-09.jpg">}}

6，打开动画蓝图的EventGraph面板
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-10.jpg">}}

然后再添加一个float属性，名字为Speed，表示角色的即时速度
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-11.jpg">}}
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-12.jpg">}}

然后再编辑事件：Event Blueprint Update Animation
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-13.jpg">}}

7，打开AnimGraph面板
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-14.jpg">}}

新建一个State Machine
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-15.jpg">}}
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-16.jpg">}}

双击State Machine，进入里面编辑。从Entry节点钟拖拽并新建一个State：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-17.jpg">}}

将该State命名为Idel/Run
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-18.jpg">}}

然后双击该State，进入里面编辑：其中Speed，就是之前新建float属性
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-19.jpg">}}
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-20.jpg">}}

最后再返回到最外层的AnimGraph面板，将StateMachine链接到Final Animation Pose上
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-21.jpg">}}

8，新建角色蓝图Character Blueprint：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-22.jpg">}}

父类选择工程中的C++ Character class：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-23.jpg">}}

然后打开角色蓝图，选中mesh
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-24.jpg">}}

将Anim Class指定为之前创建的动画蓝图：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-25.jpg">}}

将Skeletal Mesh指定为模型的骨骼：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-26.jpg">}}

如果默认的骨骼基准坐标、转向和刚体大小、MovementComponent的默认方向不匹配，则需要编辑下Mesh的Transform
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-27.jpg">}}
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-28.jpg">}}

9，到此，动画蓝图和角色蓝图编辑完成，可以在C++中使用刚刚新建的角色蓝图。

    ATopDownTestGameMode::ATopDownTestGameMode()
    {
        // use our custom PlayerController class
        PlayerControllerClass = ATopDownTestPlayerController::StaticClass();

        // set default pawn class to our Blueprinted character
        static ConstructorHelpers::FClassFinder<APawn> PlayerPawnBPClass(TEXT("/Game/TopDownCPP/Blueprints/NewBlueprint"));
        if (PlayerPawnBPClass.Class != NULL)
        {
            DefaultPawnClass = PlayerPawnBPClass.Class;
        }
    }


  
##### 补充：播放Montage的Slot问题
播放montage动画时，可能遇到播放动画没有反应的问题，例如，用C++的方式播放：

    float ACharacter::PlayAnimMontage(class UAnimMontage* AnimMontage, float InPlayRate, FName StartSectionName)


__原因__：  
可能时没有指定Montage的Slot

__解决办法__：  
1，打开Montage动画，看下默认的Slot名字叫什么
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-29.jpg">}}

2，然后在动画蓝图钟的AnimGraph中，拉出一个Slot节点
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-30.jpg">}}

然后在从该Slot中连接到Final Animation Pose中：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-31.jpg">}}

如果想修改该Slot节点的Slot名字，可以在属性面板中修改：
{{< figure src="/img/20170617-[UE4]动画蓝图的编辑流程(Animation Blueprint)/[UE4]动画蓝图的编辑流程(Animation Blueprint)-32.jpg">}}

如何在C++代码中指定Montage的Slot名字，还没研究过。但是可以通过AnimSequence动态创建一个Montage对象，并指定Slot名字：

    USkeletalMeshComponent *Mesh = MyActor->FindComponentByClass<USkeletalMeshComponent>();
    if (Mesh)
    {
        UAnimInstance *AnimInst = Mesh->GetAnimInstance();
        if (AnimInst)
        {
            UAnimMontage* Mtg = AnimInst->PlaySlotAnimationAsDynamicMontage(MyAnimSequence, TEXT("MySlotName"), 0.1f, 0.1f, 1.0f, 30.0f);
        }
    }

