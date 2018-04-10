+++
title= "[Build]cmake设置编译输出路径"
date= "2018-04-10T12:25:28+08:00"
categories= ["Build"]
tags= ["CMake"]
+++

在CMakeList.txt中如下设置后，无论是编译可执行文件还是编译静态库，都会输出到指定目录下，而不再是默认的当前目录。

    # etc. etc.
    set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "lib/")

参考自：https://stackoverflow.com/questions/38445335/cmake-library-output-directory-not-affected-by-cmake-library-output-director/38450844