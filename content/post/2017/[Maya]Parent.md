+++
title= "[Maya]Parent"
date= "2017-08-30T15:39:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++

##### 创建Parent

打开Outliner，选中需要执行Parent操作的物体。
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-01.jpg">}}

{{< alert info >}}
如果是两个物体，则第一个被选中的物体会被作为子物体；  
如果是三个及三个以上物体，则第一个被选中物体会被作为父物体，其他的作为子物体。
{{< /alert >}}

选中后在点击：Edit -》 Parent（快捷键P）。
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-02.jpg">}}
{{< figure src="/img/20170830-[Maya]Parent/[Maya]Parent-03.jpg">}}
子物体执行Transform，父物体不会变换，但父物体执行Transform，所有物体都会变换。

##### 取消Parent

选中父物体和子物体后，按：Shift + P。

***
`东风夜放花千树，更吹落、是如雨。---辛弃疾《青玉案 元夕》`