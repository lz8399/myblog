+++
title= "[Build]cmake常用配置项"
date= "2018-04-10T12:25:28+08:00"
categories= ["Build"]
tags= ["CMake"]
+++


##### 设置编译输出路径
在CMakeList.txt中如下设置后，无论是编译可执行文件还是编译静态库，都会输出到指定目录下，而不再是默认的当前目录。

    # etc. etc.
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "lib/")

参考自：https://stackoverflow.com/questions/38445335/cmake-library-output-directory-not-affected-by-cmake-library-output-director/38450844

##### 获取指定目录下的所有源文件

    file(GLOB cpp_files ./src/*.cpp)
    add_library(mylib STATIC ${cpp_files})
	
##### 打印log

	if (NOT CMAKE_VERSION VERSION_GREATER "3.0")
		message(FATAL_ERROR "cmake version 3.x is required!")
	endif()

##### 修改默认的CMAKE_MODULE_PATH目录

CMAKE_MODULE_PATH是供`find_package`搜索第三方库用的。cmake的默认Modules目录在安装目录中：`cmake-3.11.3-win64-x64\share\cmake-3.11\Modules`。  
如果要追加Modules目录，有3种方式：

	set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_PATH}:${CMAKE_MODULE_PATH}")

	LIST(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_PREFIX}")

	set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

	
##### find_package用法

通常情况下，包含第三方库需要写以下内容

	include_directories("${project_root_path}/include/")  
	link_directories(./lib)
	add_executable(myapp myapp.cpp)
	target_link_libraries(myapp mylib)  
	
如果引用的很多个第三方库，那么类似上面的内容会写很多，且如果自己的多个项目都引用了某个第三方库，那么我每个项目的`CmakeList.txt`都得写一遍，重复劳动很多。那么有没办法为每个第三方库只定义一次它的头文件和库文件信息，然后在自己的工程中只指定名称即可？（类似编译Java的Maven仓库）答案是当然可以，`find_package`帮你解决。


`find_package`定义在自己工程的CmakeList.txt中：

	find_package( XXX CONFIG REQUIRED )

然后cmake就会在默认的Modules(即`CMAKE_MODULE_PATH`指定的目录)目录中搜索这个XXX第三方库。  
搜索有两种模式：`FindXXX.cmake`和`XXXConfig.cmake`。前者叫做**Module模式**，后者叫做**Config模式**。

+ Module模式  
搜索CMAKE_MODULE_PATH指定路径下的FindXXX.cmake文件，通过该文件从而找到XXX库的头文件和lib文件位置。FindXXX.cmake中需要定义`XXX_INCLUDE_DIRS`和`XXX_LIBRARIES`。
+ Config模式  
搜索XXX_DIR指定路径下的XXXConfig.cmake文件（XXX_DIR定义在自己工程的CMakeList.txt或者cmake-gui的环境变量中），通过该文件从而找到XXX库的头文件和lib文件位置。XXXConfig.cmake中需要定义`XXX_INCLUDE_DIRS`和`XXX_LIBRARIES`

Config模式示例：  
先在自己工程的CMakeList.txt中添加

	set(XXX_DIR D:/sdk/XXX-0.9.9.0/bin)
	find_package( XXX CONFIG REQUIRED )
	
其中`CONFIG`表示使用Config模式搜索，默认是Module模式；然后D:/sdk/XXX-0.9.9.0/cmake目录下必须存在XXXConfig.cmake文件，否则当执行cmake时会提示找不到XXXConfig.cmake。

{{< alert danger>}}
XXXConfig.cmake和XXXTargets.cmake都不是手动编写的，而是CMake自动生成的！！
{{< /alert >}}

生成Config.cmake的参考代码：  
https://github.com/g-truc/glm/blob/0d973b40a49e550b1ea7df22a8573bc5fff84f24/CMakeLists.txt#L175

生成Targets.cmake的参考代码：  
https://github.com/g-truc/glm/blob/0d973b40a49e550b1ea7df22a8573bc5fff84f24/CMakeLists.txt#L198

***
`伦常乖舛，立见消亡；德不配位，必有灾殃。----《朱子家训》`