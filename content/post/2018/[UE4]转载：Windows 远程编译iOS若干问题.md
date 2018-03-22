+++
title= "[UE4]转载：Windows 远程编译iOS若干问题"
date= "2018-03-16T18:35:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "iOS building"]
+++

原文  
http://ios.tedu.cn/data/notes/276329.html

##### 问题一

    ssh_exchange_identification: Connection closed by remote hostrsync: connection unexpectedly closed (0 bytes received so far) [sender]rsync error: error in rsync protocol data stream (code 12) at /home/lapo/packaging/rsync-3.0.4-1/src/rsync-3.0.4/io.c(632) [sender=3.0.4]

解决方法

首先保证远程机器 OSX 上的 ssh 并发数配置足够，使用命令查看

    grep MaxStartups /etc/ssh/sshd_config

一般输出如下格式 10/20/30 意思是连接达到10之后以20%的概率拒绝新连接直到30为止，可以根据需求调大第一个值并重启

其次保证 RemoteToolChainPrivate.key 文件存在于 C:\Users\用户名\AppData\Roaming\Unreal Engine\UnrealBuildTool\SSHKeys\远程机器地址\mac 文件夹下，没有的话需要在 Edit -> Project Settings... -> Platforms -> iOS -> Build 中进行配置，配置好远程 OSX 机器的地址，用户名，然后点击 Generate SSH Key 生成

##### 问题二

编译失败，出现如下错误

    clang: error: argument unused during compilation: '-fno-objc-exceptions' [-Werror,-Wunused-command-line-argument]

解决方法

修改 Engine\Source\Programs\UnrealBuildTool\Platform\IOS\IOSToolChain.cs 文件，在 GetCompileArguments_Global 函数中增加 Result += " -Wno-unused-command-line-argument"; 禁用这个错误警告

##### 问题三

出 Shipping 包出现链接错误，如下

    ld: bitcode bundle could not be generated because '/Users/mac/UE4/Builds/xxx/Engine/Source/ThirdParty/PLCrashReporter/plcrashreporter-master-5ae3b0a/IOS/Release/libCrashReporter-iphoneos.a(libCrashReporter-iphoneos.a-arm64-master.o)' was built without full bitcode. All object files and libraries for bitcode must be generated from Xcode Archive or Install build for architecture arm64clang: error: linker command failed with exit code 1 (use -v to see invocation)

解决方法

目前的解决方法是在 Edit -> Project Settings... -> Platforms -> iOS -> Build 中取消 Support bitcode in Shipping

##### 问题四

IPA 打包失败，错误如下

    IPP ERROR: Application exception: System.Security.Cryptography.CryptographicException ...

解决方法

Edit -> Project Settings... -> Platforms -> iOS -> Mobile Provision 中添加描述文件和证书，或者直接打开 Engine\Binaries\DotNET\IOS\IPhonePackager.exe 进行添加

描述文件和证书生成见官方文档
