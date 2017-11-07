+++
title= "[Maya][UV]Cut and Sew"
date= "2017-11-05T13:23:40+08:00"
categories= ["Maya"]
tags= ["Modeling", "UV"]
keywords= ["Maya", "分UV", "展UV", "Cut", "Sew", "裁切", "缝合", "焊接"]
+++

Maya版本为2018.1

UV Toolkit面板钟展开Cut and Sew选项
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-01.jpg">}}

##### Auto-Seams 自动接缝
按住shift键点击Auto-Seams，弹出参数面板
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-02.jpg">}}

参数说明

+ Seams：是直接帮你裁切好，还是只是帮你选中可裁切的边，默认是Cut直接裁切。
+ Method：接缝方式，是自动，还是沿着硬边裁切。
+ Shell Splittings Tolerance：一个UV壳（shell）被裁切多个UV壳的可能性，0到1。相当于你预估一个现有的UV shell有多大的可能行被裁切。
+ Connect Holes：是否自动补洞，自动补洞可以减少扭曲。

##### Cut（UV裁切）
先选中要裁切的边线
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-03.jpg">}}
然后点击Cut，则会以这条边线为边界，裁切出一个新的UV壳。
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-04.jpg">}}

##### Cut Tool（UV裁切工具）
先点击Cut Tool之后，再单击需要裁切的边线，这样就可以边点击边裁切UV。
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-05.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-06.jpg">}}
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-07.jpg">}}

##### Sew（UV缝合）
假设要风格的位置如下
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-08.jpg">}}
先选择要缝合的边线
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-09.jpg">}}
然后点击Sew。
{{< figure src="/img/20171105-[Maya][UV]Cut and Sew/[Maya][UV]Cut and Sew-10.jpg">}}