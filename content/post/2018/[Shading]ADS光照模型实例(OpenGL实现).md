+++
title= "【Shading】ADS光照模型实例(OpenGL实现)"
date= "2018-06-03T22:30:40+08:00"
categories= ["Shading"]
tags= ["Shading", "OpenGL"]
mathjax= ["ture"]
keywords= ["Shading", "OpenGL", "ADS"]
+++

keywords：ambient diffuse specular、Phong Shading、Phong reflection model

#### 公式概述

ADS光照模型又称为“冯氏反射模型”(Phong reflection model)，为什么叫冯氏：

{{< alert info >}}
裴祥风（Bùi Tường Phong音译, 1942年—1975年），美国电脑CG研究学者，于越南出生。他于1973年在尤他大学取得哲学博士学位，并发明了Phong反射模型及Phong著色法，并广为CG界采用。1975死于白血病。
{{< /alert>}}

ADS光照模型公式缩写：

	LightIntensity = Ambient + Diffuse + Specular;
	
参数说明：

+ Ambient 环境光
+ Diffuse 漫反射
+ Specular 全反射光 / 镜面光

三个参数渲染效果示例：
{{< figure src="/img/20180603-[Shading]ADS光照模型实例(OpenGL实现)/[Shading]ADS光照模型实例(OpenGL实现)-04.jpg">}}

三个参数拆解如下：

	Ambient = La * Ka;
	Diffuse = Ld * Kd * max( dot(s, n), 0.0 );
	Specular = Ls * Ks * pow( max( dot(r, v), 0.0 ), f );

参数说明：
	
+ La 环境光强度(Ambient light intensity)
+ Ka 材质环境光反射率 / 材质环境光反射系数(Ambient reflectivity)
+ Ld 漫射光强度 / 散射光强度(Diffuse light intensity)
+ Kd 材质漫反射率 / 材质漫反射系数(Diffuse reflectivity)
+ s 顶点 / 曲面点 到光源方向的单位向量(Direction from the surface point to the light source)
+ n 顶点 / 曲面点 的法线单位向量(Normal vector at the surface point)
+ Ls 镜面光强度 / 全反射光强度(Specular light intensity)
+ Ks 材质镜面反射率 / 材质镜面反射系数(Specular reflectivity)
+ r 完全反射向量( the vector of perfect reflection)
+ v 顶点 / 曲面点 到摄像机方向的向量( the vector towards the viewer)
+ f 镜面高光(specular highlights)，值范围在1到200之间，值越小，镜面亮点越大

{{< figure src="/img/20180603-[Shading]ADS光照模型实例(OpenGL实现)/[Shading]ADS光照模型实例(OpenGL实现)-02.png">}}

光源出射强度 / 出射光强度(Intensity of the outgoing light ) `I` 的完整计算公式如下：
$$
I = La \cdot Ka+Ld \cdot Kd \cdot \left(\vec{s} \cdot \vec{n}\right)+Ls \cdot Ks \cdot \left(\vec{r} \cdot \vec{v}\right)^f
$$

#### 渲染实例

OpenGL API 版本为4.1。

假设不考虑环境光和镜面光，只考虑漫射光，渲染效果：

{{< figure src="/img/20180603-[Shading]ADS光照模型实例(OpenGL实现)/[Shading]ADS光照模型实例(OpenGL实现)-01.jpg">}}

shader 代码：  
diffuse.vert

	#version 410

	layout (location = 0) in vec3 VertexPosition;
	layout (location = 1) in vec3 VertexNormal;

	out vec3 LightIntensity;

	uniform vec4 LightPosition; // Light position in eye coords.
	uniform vec3 Kd;            // Diffuse reflectivity
	uniform vec3 Ld;            // Diffuse light intensity

	uniform mat4 ModelViewMatrix;
	uniform mat3 NormalMatrix;
	uniform mat4 ProjectionMatrix;
	uniform mat4 MVP;

	void main()
	{
		vec3 tnorm = normalize( NormalMatrix * VertexNormal);
		vec4 eyeCoords = ModelViewMatrix * vec4(VertexPosition,1.0);
		vec3 s = normalize(vec3(LightPosition - eyeCoords));

		LightIntensity = Ld * Kd * max( dot( s, tnorm ), 0.0 );

		gl_Position = MVP * vec4(VertexPosition,1.0);
	}

diffuse.frag
	
	#version 410

	in vec3 LightIntensity;

	layout( location = 0 ) out vec4 FragColor;

	void main() {
		FragColor = vec4(LightIntensity, 1.0);
	}
	
同时计算环境光、漫反射、镜面反射的渲染效果：
{{< figure src="/img/20180603-[Shading]ADS光照模型实例(OpenGL实现)/[Shading]ADS光照模型实例(OpenGL实现)-03.jpg">}}

shader 代码：  
phong.vert

	#version 410

	layout (location = 0) in vec3 VertexPosition;
	layout (location = 1) in vec3 VertexNormal;

	out vec3 LightIntensity;

	struct LightInfo {
	  vec4 Position; // Light position in eye coords.
	  vec3 La;       // Ambient light intensity
	  vec3 Ld;       // Diffuse light intensity
	  vec3 Ls;       // Specular light intensity
	};
	uniform LightInfo Light;

	struct MaterialInfo {
	  vec3 Ka;            // Ambient reflectivity
	  vec3 Kd;            // Diffuse reflectivity
	  vec3 Ks;            // Specular reflectivity
	  float Shininess;    // Specular shininess factor
	};
	uniform MaterialInfo Material;

	uniform mat4 ModelViewMatrix;
	uniform mat3 NormalMatrix;
	uniform mat4 ProjectionMatrix;
	uniform mat4 MVP;

	void main()
	{
		vec3 tnorm = normalize( NormalMatrix * VertexNormal);
		vec4 eyeCoords = ModelViewMatrix * vec4(VertexPosition,1.0);
		vec3 s = normalize(vec3(Light.Position - eyeCoords));
		vec3 v = normalize(-eyeCoords.xyz);
		vec3 r = reflect( -s, tnorm );
		float sDotN = max( dot(s,tnorm), 0.0 );
		vec3 ambient = Light.La * Material.Ka;
		vec3 diffuse = Light.Ld * Material.Kd * sDotN;
		vec3 spec = vec3(0.0);
		if( sDotN > 0.0 )
		   spec = Light.Ls * Material.Ks *
				  pow( max( dot(r,v), 0.0 ), Material.Shininess );

		LightIntensity = ambient + diffuse + spec;
		gl_Position = MVP * vec4(VertexPosition,1.0);
	}

phong.frag

	#version 410

	in vec3 LightIntensity;

	layout( location = 0 ) out vec4 FragColor;

	void main() {
		FragColor = vec4(LightIntensity, 1.0);
	}

demo完整代码：  
https://github.com/dawnarc/ShadingDemo
	
***
`在各种事物的常理中，爱情是无法改变和阻挡的，因为就本性而言，爱只会自行消亡，任何计谋都难以使它逆转。---意大利·薄伽丘《十日谈》`