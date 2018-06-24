+++
title= "【Shading】ADS光照模型实例(OpenGL实现)"
date= "2018-06-03T22:30:40+08:00"
categories= ["Shading"]
tags= ["Shading", "OpenGL"]
mathjax= ["ture"]
keywords= ["Shading", "OpenGL", "ADS"]
+++

keywords：ambient diffuse specular、Phong Shading、Phong reflection model

ADS光照模型又称为“冯氏反射模型”(Phong reflection model)，为什么叫冯氏：

{{< alert info >}}
裴祥风（Bùi Tường Phong音译, 1942年—1975年），美国电脑CG研究学者，于越南出生。他于1973年在尤他大学取得哲学博士学位，并发明了Phong反射模型及Phong著色法，并广为CG界采用。1975死于白血病。
{{< /alert>}}

公式：

$$
Id = Ld \cdot Kd \cdot \left(\max_{\vec{s} \cdot \vec{n}, 0}\right)^f
$$
	
参数解释：

+ Id : Intensity of the outgoing light 光源出射强度 / 出射光强度
+ Ld : Intensity of the light source 光源强度
+ Kd : Reflection coefficient 反射系数
+ s :  Direction from the surface point to the light source 顶点 / 曲面点 到光源方向的单位向量
+ n :  Normal vector at the surface point 顶点 / 曲面点 的法线单位向量

***
`在各种事物的常理中，爱情是无法改变和阻挡的，因为就本性而言，爱只会自行消亡，任何计谋都难以使它逆转。---意大利·薄伽丘《十日谈》`