+++
title= "[Build]cmake-gui使用"
date= "2017-09-06T14:50:28+08:00"
categories= ["Build"]
tags= ["CMake"]
+++


要使用cmake-gui，请确保已经写好了CMakeLists.txt。
打开cmake-gui后，指定source目录和生成的bin目录。
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-01.jpg">}}

再点击Configure，指定VS版本。然后就可以生成VS工程sln等文件了。
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-02.jpg">}}

如果生成过程中有相关依赖库没有指定正确，输出窗口会给出提示，比如示例中有个glm库的没有指定，此时我们再重新指定下依赖库的位置。
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-03.jpg">}}

配置后再点击Generate，直到没有错误信息提示。
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-04.jpg">}}

##### CMAKE相关的配置说明
+ CMAKE_CONFIGURATION_TYPES**
CMAKE_CONFIGURATION_TYPES表示VS上的Solution Configurations（Debug/Release等）选项
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-05.jpg">}}

+ CMAKE_INSTALL_PREFIX
表示编译后存放的目录，以方便FIND_XXX()方式来查找。

##### 删除临时文件
如果要删除cache文件，点击：File -》 Delete Cache。
{{< figure src="/img/20170906-[Build]cmake-gui使用/[Build]cmake-gui使用-06.jpg">}}