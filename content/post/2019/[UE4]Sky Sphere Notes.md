+++
title= "[UE4]Sky Sphere Notes"
date= "2019-02-16T18:03:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Sky Sphere"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-015.jpg"
+++

Engine Default Sky Sphere:  
<!--more-->
{{< hl-text green >}}Blueprint'/Engine/EngineSky/BP_Sky_Sphere.BP_Sky_Sphere'{{< /hl-text >}}

##### How to set up Sky Sphere

{{< figure src="/img/20190216-[UE4]Sky Sphere Notes/[UE4]Sky Sphere Notes-00-01.jpg">}}
{{< figure src="/img/20190216-[UE4]Sky Sphere Notes/[UE4]Sky Sphere Notes-00-02.jpg">}}

##### How to change Sky Color

Uncheck `Colors Determined By Sun Position`, and change `Zenith Color`

{{< figure src="/img/20190216-[UE4]Sky Sphere Notes/[UE4]Sky Sphere Notes-01.jpg">}}

{{< alert warning >}}
if uncheck `Colors Determined By Sun Position`, Sky Color would affect whole scene objects.
{{< /alert >}}

##### How to change Sun Position

In Level Editor, change the rotation of Directional Light.
{{< figure src="/img/20190216-[UE4]Sky Sphere Notes/[UE4]Sky Sphere Notes-02.jpg">}}
Then click `Refresh Material` of Sky Sphere.
{{< figure src="/img/20190216-[UE4]Sky Sphere Notes/[UE4]Sky Sphere Notes-03.jpg">}}

Reference: How to change basic sun position in editor (not PIE)?  
https://answers.unrealengine.com/questions/317372/how-to-change-basic-sun-position-in-editor-not-pie.html


***
`快乐属于那些选择了孤独的人，因为你是从那儿来的，而且你还要回到那儿去。——《托马斯福音》（GospelofThomas）`

