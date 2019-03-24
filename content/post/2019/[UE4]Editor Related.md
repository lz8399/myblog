+++
title= "[UE4]Editor Related"
date= "2019-01-18T22:05:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Sequencer"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-010.jpg"
+++

##### How to set Pivot Offset

<!--more-->

{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-01.jpg">}}
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-02.jpg">}}

##### How to override Events of Components in Blueprint

Right click component -> Add Event
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-03.jpg">}}

##### How to open optimization Viewmodes

{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-04.jpg">}}

##### How to open Buffer Visualization

{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-05.jpg">}}

##### Move directory in Editor

{{< alert danger >}}
Right clicking on the folder and selecting "Fix Up Redirectors in Folder" before trying to move it, otherwise reference of assets would be lost.
{{< /alert >}}

{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-06.jpg">}}

##### How to customize screen size of LOD

1st way:  
Screen Size that can't be modify
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-07.jpg">}}
Uncheck `Auto Compute LOD Distance` allow to modify `Screen Size`
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-08.jpg">}}

2nd way:  
Uncheck `Auto Compute LOD Distance` when import FBX asset.
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-09.jpg">}}

##### How to add Exec Pin on Macro in Blueprint

By default, Blueprint Macro has no `Exec` Pin:
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-10.jpg">}}
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-11.jpg">}}
You can add an input and output parameter which type is `Exec`:
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-12.jpg">}}
{{< figure src="/img/20190118-[UE4]Editor Related/[UE4]Editor Related-13.jpg">}}

Macros  
https://docs.unrealengine.com/en-us/Engine/Blueprints/UserGuide/Macros

##### Reference

Unreal Editor Manual  
https://docs.unrealengine.com/en-us/Engine/Editor

***
`善，没有理由战胜不了恶，只要天使们能像黑手党那样组织起来。──库尔特·冯内古特（KurtVonnegut）《没有国家的人》`