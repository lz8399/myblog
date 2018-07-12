+++
title= "[OpenGL]GLSL Cookbook源码编译步骤流程(2018.06新版)"
date= "2018-06-18T23:47:28+08:00"
categories= ["OpenGL"]
tags= ["Shading", "Graphics", "OpenGL"]
+++

去年写过一篇文章，该文章与github上的最新代码已不再有效（主要是glm和glfw相关的CMake配置发生变动）：  
https://dawnarc.com/2017/09/openglglsl-cookbook%E6%BA%90%E7%A0%81%E7%BC%96%E8%AF%91%E6%AD%A5%E9%AA%A4%E6%B5%81%E7%A8%8B/

当前这篇文章针对github的glslcookbook最新代码，重新梳理一次配置流程，保证最新代码能编译工程并跑起来。步骤如下：

1，下载glm源码，并用cmake-gui生成VS工程文件：  
https://github.com/g-truc/glm/releases/download/0.9.9.0/glm-0.9.9.0.zip

假设  
cmake-gui的source code设置为：  
`D:/sdk/glm-0.9.9.0`  
cmake-gui的build binaries设置为：  
`D:/sdk/glm-0.9.9.0/bin`

Configure过程中，会有警告，可以无视，直接Generate：

	GLM is a header only library, no need to build it. Set the option GLM_TEST_ENABLE with ON to build and run the test bench
	
生成完以后，不需要打开VS编译，后面直接使用相关文件即可。


2，下载glfw源码，并用cmake-gui生成VS工程文件。
https://github.com/glfw/glfw/releases/download/3.2.1/glfw-3.2.1.zip

假设  
cmake-gui的source code设置为：  
`D:/sdk/glfw-3.2.1`  
cmake-gui的build binaries设置为：  
`D:/sdk/glfw-3.2.1/bin`

Configure过程中，会有红色警告，可以无视，直接Generate：

	CMake Deprecation Warning at CMakeLists.txt:10 (cmake_policy):
	The OLD behavior for policy CMP0042 will be removed from a future version
	of CMake.

	The cmake-policies(7) manual explains that the OLD behaviors of all
	policies are deprecated and that a policy should be set to OLD only under
	specific short-term circumstances.  Projects should be ported to the NEW
	behavior and not rely on setting a policy to OLD.


生成完以后，打开bin/GLFW.sln，并编译整个工程。编译完成后，做以下步骤：

+ 将文件`D:\sdk\glfw-3.2.1\bin\src\Debug\glfw3.lib`拷贝到`D:\sdk\glfw-3.2.1\bin\CMakeFiles\Export\lib`
+ 将目录`D:\sdk\glfw-3.2.1\include`拷贝到`D:\sdk\glfw-3.2.1\bin\CMakeFiles\Export\`
+ 将文件`D:\sdk\glfw-3.2.1\bin\src\glfw3Config.cmake`拷贝到`D:\sdk\glfw-3.2.1\bin\CMakeFiles\Export\lib\cmake\glfw3`

3，克隆glslcookbook代码：  
https://github.com/daw42/glslcookbook

然后打开CMakeList.txt，在find_package之前追加两行（注意：斜杠方向向右）：

	set(glm_DIR D:/sdk/glm-0.9.9.0/bin)
	set(glfw3_DIR D:/sdk/glfw-3.2.1/bin/CMakeFiles/Export/lib/cmake/glfw3)

然后用cmake-gui生成VS工程文件，然后打开VS编译工程，并运行相关demo即可。例如：

	D:\glslcookbook\bin\chapter02>start Debug/chapter02.exe ads
	
***
`人就是要以自卑为跳板，才能跳得更高。---坂田银时《银魂》`