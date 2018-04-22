+++
title= "[UE4]UMG Image ‘Draw as’ Type"
date= "2018-04-17T16:34:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Image Draw as"]
+++


添加一个Button，大小设置为300x300
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-01.jpg">}}
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-02.jpg">}}

##### Image
当Draw As设置为Image时，图片会被整体拉伸
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-03.jpg">}}
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-04.jpg">}}

##### Box
图片会被分成九宫格（3x3），其中4个脚的格子大小固定，不会随分辨率改变而拉伸，上下边沿格子会跟随分辨率横向拉伸，左右边沿格子会跟随分辨率纵向拉伸
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-05.jpg">}}

##### Border
Border模式，Margin设置为0.25
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-06.jpg">}}
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-07.jpg">}}

Border模式，Margin设置为0.5
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-08.jpg">}}
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-09.jpg">}}

{{< alert info >}}
Marin表示Image边沿格子的大小，数值是百分比。例如，假设Margin设置为0.5，则表示边沿格子的大小为图片的50%。
{{< /alert >}}

Border模式下，Image不会随着屏幕大小拉伸，而是固定大小。例如，当Margin为0.5，且Viewport变小时，每个格子的图片不会被拉伸：
{{< figure src="/img/20180417-[UE4]UMG Image ‘Draw as’ Type/[UE4]UMG Image ‘Draw as’ Type-10.jpg">}}