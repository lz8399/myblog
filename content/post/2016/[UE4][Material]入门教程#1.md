---
title: "[UE4][Material]入门教程01"
date: "2016-11-23T23:24:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Material
---

{{< figure src="/img/20161123-[UE4][Material]入门教程01/[UE4][Material]入门教程01-01.jpg">}} 

UE3的材质由3个参数组成：Diffuse、Specular、SpecPower。
UE4的材质不在沿用UE3的特性，基本参数有：

`BaseColor`：基本颜色

`Metallic`：金属质感

`Specular`：高光强度

`Roughness`：粗糙度

`EmissiveColor`：自发光颜色


注意事项：
1，	只有材质为非金属时（Metallic为0.0），Specular才起作用


Start Content自带的典型材质文件：
M_Wood_Floor_Walnut_Worn
这个材质演示了材质常用属性和函数。

**Specular不同值下的渲染效果：**

0： 
{{< figure src="/img/20161123-[UE4][Material]入门教程01/[UE4][Material]入门教程01-02.jpg">}} 

0.3： 
{{< figure src="/img/20161123-[UE4][Material]入门教程01/[UE4][Material]入门教程01-03.jpg">}} 

1.0： 
{{< figure src="/img/20161123-[UE4][Material]入门教程01/[UE4][Material]入门教程01-04.jpg">}} 
