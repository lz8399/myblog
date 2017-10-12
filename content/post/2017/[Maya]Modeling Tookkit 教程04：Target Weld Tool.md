+++
title= "[Maya]Modeling Tookkit 教程04：Target Weld Tool"
date= "2017-10-05T20:30:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
+++


Maya版本为2018

{{< alert danger >}}注意：执行Target Weld之前，情确保需要缝合的两个点是同一个Object（可以通过Mesh -》 Combine将两个Object合并为一个Object），否则无法缝合。{{< /alert >}}

假设有这样一个模型
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-01.jpg">}}

选中Target Weld
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-02.jpg">}}
然后鼠标左键按住起始顶点不放
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-03.jpg">}}

然后往目标顶点拖动，等到出现黄圈后再松开。
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-04.jpg">}}

这样就缝合完成。
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-05.jpg">}}

为了确保缝合成功，可以拖动试一下，看两个顶点的位置有没同时移动。
{{< figure src="/img/20171005-[Maya]Modeling Tookkit 教程04：Target Weld Tool/[Maya]Modeling Tookkit 教程04：Target Weld Tool-06.jpg">}}
也可以按数字键3看平滑效果是否正常，如果有点没有缝合，平滑时的效果会很奇怪。