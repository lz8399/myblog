+++
title= "[UE4]静态链接Protobuf 3.x版本的错误"
date= "2017-12-09T16:44:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Error", "Protobuf"]
+++


UE4集成protobuf时建议使用2.x版本。如果使用3.x，将protoc生成的代码打成lib链接到UE4工程时，会出现以下错误（当template文件中有string字段时会报错，如果没有string可以编译通过）：

	2>TestTDGameMode.cpp.obj : error LNK2019: unresolved external symbol "public: void __cdecl my_proto::login_info::set_account(char const *)" (?set_account@login_info@fh_proto@@QEAAXPEBD@Z) referenced in function "public: virtual void __cdecl ATestTDGameMode::BeginPlay(void)" (?BeginPlay@ATestTDGameMode@@UEAAXXZ)
	2>G:\Source\Work\Game20171205\program\client\TestTD\Binaries\Win64\UE4Editor-TestTD-4710.dll : fatal error LNK1120: 1 unresolved externals

有人写了py脚本来生成UE4风格的C++代码，在UE4工程中源码编译protobuf 3.x，是否可行没试过：  
https://thecodeway.com/blog/?p=1394