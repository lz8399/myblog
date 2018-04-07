+++
title= "[UE4]Indirect Lighting Cache(间接光照缓存)"
date= "2018-04-02T14:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Indirect Lighting"]
+++


原文：https://home.gamer.com.tw/creationDetail.php?sn=3935067

某台湾网站上看到的文章，比起youtube上讲Indirect Lighting的视频要直观易懂。

### Indirect Lighting Cache(间接光照缓存)

官方文档  
http://api.unrealengine.com/INT/Engine/Rendering/LightingAndShadows/IndirectLightingCache/index.html

{{< hl-text primary >}}Indirect Lighting Cache是类似于Unity的LightProbe{{< /hl-text >}}，间接光照就是当光线直射到一个物体上后，光线反弹后所得到的颜色，反弹后的光线还会再去影响到周边的物体，如同白色的桌面上摆着红色的物体，物体周围会有些微的红色。

而Indirect Lighting Cache还有一种功能就是{{< hl-text primary >}}提供动态物件能获得间接光的资讯{{< /hl-text >}}，例如像是当角色靠近一面红色墙壁时，会有些微的红光反映在角色身上。

在UE4里面建构光照后会自动产生Indirect Lighting Cache，可以从编辑画面的Show > Visualize > volume light sample显示当前Indirect Lighting Cache的情形。

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-01.png">}}
显示间接光照缓存

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-02.png">}}
没有间接光照缓存的情况，角色不会受到静态灯光的颜色影响

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-03.png">}}
有间接光照缓存时，角色即会受到静态灯光影响

可以从上图看到场景中那些小正方形就是间接光照缓存的颜色，周围的物件会受到靠近的间接光照颜色影响。

### Lightmass Importance Volume(重要光照范围) 

官方文档  
http://api.unrealengine.com/INT/Engine/Rendering/LightingAndShadows/Lightmass/Basics/index.html

在建构光照贴图时，{{< hl-text primary >}}若场景中没有给予Lightmass Importance Volume，会对整个场景做间接光照的采样{{< /hl-text >}}，产生Indirect Lighting Cache，{{< hl-text primary >}}这对大型游戏场景是相当的浪费{{< /hl-text >}}，像是游戏角色到不了的中、远景不需要产生Indirect Lighting Cache，这时候就可以在场景中置入Lightmass Importance Volume，指定特定区域内才会产生Indirect Lighting Cache，节省不少建构光照的时间。

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-04.png">}}
Modes视窗中的Volumes页签找到Lightmass Importance Volume

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-05.png">}}
拖曳至场景后，调整Scale直到包覆特定区域即可

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-06.png">}}
建构光照后会在Lightmass Importance Volume区域内看到产生的间接光照缓存

### Lightmass Character Indirect Detail Volumes(角色细节间接光范围 )

在上述的Lightmass Importance Volume所建构出来的间接光会发现大多都只有在模型上才有，{{< hl-text primary >}}无法再浮空的地方产生间接光缓存 {{< /hl-text >}}(像是靠近天花板的地方)，主要原因是Lightmass Importance Volume是提供使用者快速建构重要范围，没有办法处理到细节的部份，因此在这种情况下会产生这种问题:

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-07.gif">}}
当角色跳跃至天花板附近时，受光会变亮

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-08.png">}}
主因是因为靠近天花板那区没有产生间接光照缓存

这时候就需要补充细节的间接光，就必须使用Lightmass Character Indirect Detail Volumes，一样在Modes里的Volumes页签中找Lightmass Character Indirect Detail Volumes，拖曳至场景后放在需要补足间接光的地方，再建构光照贴图后即可。

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-09.png">}}
Modes视窗中的Volumes页签找到Lightmass Character Indirect Detail Volumes

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-10.png">}}
包覆需要间接光细节的区域

{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-11.png">}}
建构光照后就会在该区域生成间接光照缓存


{{< figure src="/img/20180402-[UE4]Indirect Lighting Cache(间接光照缓存)/Indirect Lighting Cache(间接光照缓存)-12.gif">}}
增加了间接光后，靠近天花板会变亮的问题就解决了

Lightmass Character Indirect Detail Volumes通常会应用在垂直的地形上，像是升降梯、电梯那种，只要角色到的了的地方但却没有间接光缓存时就可以使用!