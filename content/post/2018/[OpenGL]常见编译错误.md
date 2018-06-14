+++
title= "[OpenGL]常见编译错误"
date= "2018-06-11T00:25:40+08:00"
categories= ["OpenGL"]
tags= ["OpenGL"]
keywords= ["OpenGL", "Error", "Compile"]
+++

##### 错误1

	error C2027: use of undefined type 'glm::tvec4<float,0>'
	
原因：  
只包含了头文件：`<glm/detail/type_vec.hpp>`

解决办法：  
不需要包含`<glm/detail/type_vec.hpp>`，只需要包含`<glm/glm.hpp>`。

***
`就投机钻营来说，世故的价值永远是无可比拟的。---《死魂灵》`