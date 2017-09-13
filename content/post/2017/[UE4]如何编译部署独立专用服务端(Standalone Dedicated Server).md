+++
title= "[UE4]如何编译部署独立专用服务端(Standalone Dedicated Server)"
date= "2017-02-25T20:33:40+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
draft = true
+++

keywords：UE4、Replication、Relicate、reliable、RPC、RTS Movement、Dedicated Server、属性同步

如果出现以下错误提示，原因是客户端和服务端版本不匹配，比如编译完客户端之后又改过代码，然后再编译服务端。

    LogNet: NotifyControlMessage: Client connecting with invalid version. LocalNetworkVersion: -629807355, RemoteNetworkVersion: 1642249361


