+++
title= "[Batch]Protobuf 3 protoc generate multiple proto files"
date= "2018-03-31T19:03:02+08:00"
categories= ["Batch"]
tags= ["protobuf", "batch"]
keywords= ["Protobuf 3", "protoc", "generate multiple proto files"]
+++

keywords：Protobuf 3、同时生成多个proto文件、通配符

假设目录结构如下：

    root
      |-proto
          |-a.proto
          |-b.proto
      |-build
      |-protoc.exe

protobuf 2.x版本，可以通过通配符指定所有proto模板文件

    protoc --proto_path=./proto/ --cpp_out=dllexport_decl=LIBPROTOC_EXPORT:./build ./proto/*.proto

但是protobuf 3.x版本不识别通配符，不过可以通过BAT或者shell提供的遍历语法，来同时生成多个proto文件。

windows bat：
    
    set dir=%cd%/proto

    set out_cpp=./build

    for /R %%s in (*.proto) do (
        if exist %%s protoc.exe -I=%dir% --cpp_out=%out_cpp% %%s
    )

***
`欲无祸于昭昭，勿得罪于冥冥。----《菜根谭》`
