+++
title= "[UE4]Android打包版本执行protobuf的ParseFromArray函数崩溃的问题"
date= "2018-04-21T22:01:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "protobuf-lite", "ParseFromArray", "Crash"]
+++

keywords：UE4、protobuf-lite、ParseFromArray、Crash

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
    
    