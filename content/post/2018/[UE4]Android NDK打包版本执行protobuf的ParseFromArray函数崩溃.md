+++
title= "[UE4]Android NDK打包版本执行protobuf的ParseFromArray函数崩溃"
date= "2018-04-21T22:01:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "protobuf-lite", "Android NDK","ParseFromArray", "Crash"]
+++

keywords：UE4、protobuf-lite、Android NDK、ParseFromArray、Crash

protobuf与android ndk编译后，集成到UE4中执行时，每当执行ParseFromArray时就会崩溃（Windows版本没有问题）：

    MessageTest msg;
    bool rs = msg.ParseFromArray(buffer, buffer_size);

解决办法：将ParseFromArray()函数内部的代码复制出来，放在工程的代码中，然后再执行。
    
### protobuf 2.x

    #ifndef	__ProtobufHelper_H__
    #define	__ProtobufHelper_H__

    #include <google/protobuf/message_lite.h>
    #include <google/protobuf/io/coded_stream.h>

    class ProtobufHelper
    {
    public:

        static bool Parse(::google::protobuf::MessageLite& Message, const char* Data, int Size)
        {
            ::google::protobuf::io::CodedInputStream input(reinterpret_cast<const uint8*>(Data), Size);

            return Message.MergePartialFromCodedStream(&input) && input.ConsumedEntireMessage();
        }
    };

    #endif


### protobuf 3.x

    #ifndef	__ProtobufHelper_H__
    #define	__ProtobufHelper_H__

    #include <google/protobuf/message_lite.h>
    #include <google/protobuf/io/coded_stream.h>
    #include "CoreMinimal.h"

    class ProtobufHelper
    {
    public:

        static bool Parse(::google::protobuf::MessageLite& Message, const void* Data, int Size)
        {
            ::google::protobuf::io::CodedInputStream input(static_cast<const uint8*>(Data), Size);

            Message.Clear();

            if (!Message.MergePartialFromCodedStream(&input))
            {
                return false;
            }
            
            if (!Message.IsInitialized()) 
            {
                //GOOGLE_LOG(ERROR) << InitializationErrorMessage("parse", *message);
                UE_LOG(LogTemp, Error, TEXT("protobuf message isn't initialized."));
                return false;
            }
            return true;
        }
    };

    #endif
    
### 使用示例

    MessageTest msg;
    bool rs = ProtobufHelper::Parse(msg, buffer, buffer_size);
    
### message嵌套问题

{{< alert danger >}}
protobuf 3.x版本，如果在一个模版文件中定义多个message，即使用上面的Parse函数，UE4打包Android版本运行时也会导致崩溃。2.x版本正常
{{< /alert >}}

SearchResponse.proto

	syntax = "proto3";
	
	option optimize_for = LITE_RUNTIME;

	message SearchResponse {
	  repeated Result results = 1;
	}

	message Result {
	  string url = 1;
	  string title = 2;
	  repeated string snippets = 3;
	}
	
解决办法：一个proto文件只定义一种message，通过import方式导入。

SearchResponse.proto

	syntax = "proto3";
	
	option optimize_for = LITE_RUNTIME;
	
	import "Result.proto";

	message SearchResponse {
	  repeated Result results = 1;
	}

Result.proto

	syntax = "proto3";
	
	option optimize_for = LITE_RUNTIME;

	message Result {
	  string url = 1;
	  string title = 2;
	  repeated string snippets = 3;
	}

***
`当才华无法撑起野心时，应静下心学习。`