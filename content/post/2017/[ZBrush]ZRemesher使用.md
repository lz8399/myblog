---
title: "[ZBrush]ZRemesher使用"
date: "2017-05-07T21:50:40+08:00"
categories:
- ZBrush
tags:
- ZBrush
- Modeling
- Sculpting
---

Keywords：ZBrush、ZRemesher、Project All

假如我们的模型的布线被拉的很乱了：
{{< figure src="/img/20170507-[ZBrush]ZRemesher使用/[ZBrush]ZRemesher使用-01.jpg">}}

此时点击下：Tool -》 Geometry -》 ZRemesher -》 ZRemesher。
{{< figure src="/img/20170507-[ZBrush]ZRemesher使用/[ZBrush]ZRemesher使用-02.jpg">}}

稍微等待一下后（取决于DynaMesh的分辨率），就可以重新生成非常简洁的布线：
{{< figure src="/img/20170507-[ZBrush]ZRemesher使用/[ZBrush]ZRemesher使用-03.jpg">}}

ZRemesher控制模型精度的两个参数为：Target Polygons Count、AdaptiveSize。
{{< figure src="/img/20170507-[ZBrush]ZRemesher使用/[ZBrush]ZRemesher使用-04.jpg">}}

##### 实际用途：
ZRemesher可以用于模型的自动拓扑：先在SubTool复制一个模型，然后使用ZRemesher生成一个低分辨率的模型，然后再使用Project All功能，就可以进行自动拓扑了，可以参见之前的文章：
[ZBrush]Project All实例(example)
http://www.dawnarc.com/2017/04/zbrushproject-all%E5%AE%9E%E4%BE%8Bexample/


