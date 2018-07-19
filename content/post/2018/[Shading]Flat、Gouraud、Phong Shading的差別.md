+++
title= "[Shading]Flat、Gouraud、Phong Shading的差別"
date= "2018-06-26T15:54:40+08:00"
categories= ["Shading"]
tags= ["Shading"]
keywords= ["Shading", "Flat、Gouraud、Phong"]
+++

keywords：Comparison flat, Gouraud, Phong shading

原文：  
https://cg2010studio.com/2011/11/01/flat%E3%80%81gouraud%E3%80%81phong-shading%E7%9A%84%E5%B7%AE%E5%88%A5-comparison-flat-gouraud-phong-shading/

现今多边形的著色方法基本的有这三种：**flat**、**Gouraud**、**Phong Shading**，它们之间有何差别呢？喜欢玩游戏的人一定要知道Gouraud Shading，这是PC最常使用的著色法，因为效能好、效果还不错。而近年来，随着GPU快速的发展，Phong Shading逐渐应用在更真实的著色上。

从一张图可以看出他们的各自的特色：（a: Flat→b: Gouraud→c: Phong）

{{< figure src="/img/20180626-[Shading]Flat、Gouraud、Phong Shading的差別/[Shading]Flat、Gouraud、Phong Shading的差別-01.jpg">}}

从古早到现代：Flat→Gouraud→Phong Shading。

从简单到复杂：Flat→Gouraud→Phong Shading。

观察三者所呈现的效果，可以归纳出下列结论：

+ 平面着色：恒定的表面着色
+ Gouraud着色：颜色插值着色
+ Phong着色：顶点法线插值着色

用简单的中文来解释**原理**：

+ flat shading：三角形的顶点没有法向量，三角形整个面才有法向量，打光时整个三角形只呈现一种颜色。
+ Gouraud shading：三角形的顶点都有各自的法向量，打光时三个顶点有各自的颜色，接着做双线性内插（bilinear interpolation）来求得颜色，使整个三角形有渐层的颜色变化。
+ Phong shading：三角形的顶点都有各自的法向量，先对三角形整个面作法向量的双线性内插，接着打光来求整个三角形的颜色。

然后我们来分析各自的**复杂度**：

假设三角形面积为 `A` 。三角形个数为 `N` 。而且我们知道打一次光需要6次乘法和2次加法和1次查表的运算，此设定为 `L` 。双线性内插设定为 `B` 。

+ flat shading的复杂度：N * L
+ Gouraud shading  的复杂度：N * (3 * L + b * A)
+ Phong shading的复杂度：(B + L) * N * A

数学好的人很容易计算出复杂度：Flat < Gouraud < Phong Shading。这里也因此说明了为何早期电脑都只支援Gouraud shading，就算已经知道Phong shading的效果比Gouraud shading好，但还是选择效能好而效果不错的Gouraud shading！如今GPU发展迅速，Phong Shading的效能已得到提升。
{{< figure src="/img/20180626-[Shading]Flat、Gouraud、Phong Shading的差別/[Shading]Flat、Gouraud、Phong Shading的差別-02.png">}}

##### stack overflow答案
https://computergraphics.stackexchange.com/questions/377/shading-phong-vs-gouraud-vs-flat

Flat shading is the simplest shading model. Each rendered polygon has a single normal vector; shading for the entire polygon is constant across the surface of the polygon. With a small polygon count, this gives curved surfaces a faceted look.

Phong shading is the most sophisticated of the three methods you list. Each rendered polygon has one normal vector per vertex; shading is performed by interpolating the vectors across the surface and computing the color for each point of interest. Interpolating the normal vectors gives a reasonable approximation to a smoothly-curved surface while using a limited number of polygons.

Gourard shading is in between the two: like Phong shading, each polygon has one normal vector per vertex, but instead of interpolating the vectors, the color of each vertex is computed and then interpolated across the surface of the polygon.

On modern hardware, you should either use flat shading (if speed is everything) or Phong shading (if quality is important). Or you can use a programmable-pipeline shader and avoid the whole question.

***
`你要做一个可爱的人，不烦世事，满心欢喜，别恃宠而骄，别卑贱讨好。`
