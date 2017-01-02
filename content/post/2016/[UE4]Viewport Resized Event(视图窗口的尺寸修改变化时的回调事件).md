+++
title= "[UE4]Viewport Resized Event(视图窗口的尺寸修改变化时的回调事件)"
date= "2016-06-18T00:25:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
+++


1，在BeginPlay()函数中添加绑定事件：

    GEngine->GameViewport->Viewport->ViewportResizedEvent.AddUObject(this, &MyObj::MyFunction);

2，编写回调逻辑。注意，回调函数必须包含FViewport*和uint32两个参数

    void MyObj::MyFunction(FViewport* ViewPort, uint32 val)
    {
    }