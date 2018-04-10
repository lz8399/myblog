+++
title= "[UE4]TouchInterface ZOrder"
date= "2018-03-31T19:03:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "TouchInterface"]
+++

##### 顺序从低到高

Player Screen  
+ Player Screen Widgets  

Viewport  
+ Touch Interface  
+ Viewport Widgets  

##### 实际应用
比如创建一个UserWidget，一般是AddToViewport，这样会导致UMG遮挡TouchInterface输入，如果希望TouchInterface优先UMG接收Input事件，那么可以将该UserWidget添加到PlayerScreen中：

    LoginWidget->AddToPlayerScreen();


##### 其他参考
Create widget in pure C++  
https://forums.unrealengine.com/development-discussion/android-development/78992-default-touch-interface-zorder