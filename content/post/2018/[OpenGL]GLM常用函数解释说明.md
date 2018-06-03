+++
title= "[OpenGL]GLM常用函数解释说明"
date= "2018-06-03T22:57:40+08:00"
categories= ["OpenGL"]
tags= ["OpenGL"]
keywords= ["OpenGL", "Function", "Comment"]
+++

GLM默认使用右手坐标系，如果要改成默认左手坐标系，使用：

	GLM_FORCE_LEFT_HANDED

#### \<glm/trigonometric.hpp\>

	GLM_FUNC_DECL GLM_CONSTEXPR vec< L, T, Q > radians (vec< L, T, Q > const &degrees)
	
将角度转化为弧度。

***

#### \<glm/gtx/transform.hpp\>

	GLM_FUNC_DECL mat< 4, 4, T, Q > rotate (T angle, vec< 3, T, Q > const &v)
	
使用一个用弧度(radians)表示的角度(degrees)，以及一个用3个标量(scalar)表示的坐标(axis)，来构建一个4X4的旋转矩阵(rotate matrix)。

#### \<glm/gtc/matrix_transform.hpp\>

	GLM_FUNC_DECL mat<4, 4, T, Q> lookAt (vec<3, T, Q> const &eye, vec<3, T, Q> const &center, vec<3, T, Q> const &up)
	
基于默认的偏手坐标系来构建一个给定视图矩阵(view matrix)的视角(look)
***

	GLM_FUNC_DECL mat<4, 4, T, defaultp> perspective (T fovy, T aspect, T near, T far)
	
为一个对称透视图截锥(symmetric perspective-view frustum)创建矩阵，基于默认的偏手坐标系和默认的近剪裁面距离、远剪裁面距离

参数说明：

+ fovy 相机视角宽度
+ aspect 长宽比率
+ near 近面裁剪距离
+ far 远面裁剪距离

如果要修改默认的近/远剪裁面，使用：

	 GLM_FORCE_DEPTH_ZERO_TO_ONE

***

### 参考
GLM Manual  
https://github.com/g-truc/glm/blob/master/manual.md

GLM API documenation  
https://glm.g-truc.net/0.9.9/api/modules.html

***
`强迫经常使热恋的人更加铁心，而从来不能叫他们回心转意。---德国·席勒《阴谋与爱情》`