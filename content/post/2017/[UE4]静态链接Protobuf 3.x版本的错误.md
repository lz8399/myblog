+++
title= "[UE4]静态链接Protobuf 3.x版本的错误"
date= "2017-12-09T16:44:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Error", "Protobuf"]
+++


如果使用3.x，将protoc生成的代码打成lib链接到UE4工程时，会出现以下错误（当template文件中有string字段时会报错，如果没有string可以编译通过）：

	2>TestTDGameMode.cpp.obj : error LNK2019: unresolved external symbol "public: void __cdecl my_proto::login_info::set_account(char const *)" (?set_account@login_info@fh_proto@@QEAAXPEBD@Z) referenced in function "public: virtual void __cdecl ATestTDGameMode::BeginPlay(void)" (?BeginPlay@ATestTDGameMode@@UEAAXXZ)
	2>G:\Source\Work\Game20171205\program\client\TestTD\Binaries\Win64\UE4Editor-TestTD-4710.dll : fatal error LNK1120: 1 unresolved externals

Python脚本对protoc生成代码二次转换，然后与UE4工程编译(Protobuf 3.x)
https://github.com/thejinchao/libprotobuf  
https://thecodeway.com/blog/?p=1394

修改Protobuf 3.x源码并作为UE4 plugin编译  
https://github.com/jashking/UE4Protobuf  
{{< hl-text green >}}我基于该项目的protobuf代码，做了一个cmake自动构建配置：{{< /hl-text >}}  
https://github.com/dawnarc/protobuf_ue4_cmake

将protobuf3.x作为插件集成进UE4  
https://github.com/marshal-it/Protobuffer_UE4

如果使用protobuf 2.x版本，可以不用修改任何代码，直接作为一个lib链接UE4工程。

***
`景色如冬`  
`萧瑟如枫`  
`攻势如弓`  
`魂断犹如梦中`  
`----《黄金甲》`