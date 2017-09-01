+++
title= "[Maya]Parent"
date= "2017-08-30T15:39:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++


打开Outliner，选中需要执行Parent操作的物体。
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-01.jpg">}}

<font color=red>需要同时选中多个，如果只选择一个无法执行Parent。且最先选中的哪个物体，则该物体会被当作父节点，其他物体当作子节点。</font>

选中后在点击：Edit -》 Parent。
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-02.jpg">}}
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-03.jpg">}}
子物体执行Transform，父物体不会变换，但父物体执行Transform，所有物体都会变换。