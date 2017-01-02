---
title: "[UE4]客户端无法调用FindPathToLocationSynchronously函数的问题"
date: "2016-06-13T12:02:02+08:00"
categories:
- UnrealEngine4
tags:
- error
- UE4
---

如果client-side执行UNavigationSystem::FindPathToLocationSynchronously()，会返回错误：

    Error Accessed None 'CallFunc_FindPathToLocationSynchronously_ReturnValue2' from node ReturnNode in blueprint GameController

### 原因：
client-side默认关闭了寻路功能，需要启动，修改设置：Project Settings > Navigation System > bAllowClientSideNavigation

参考：https://answers.unrealengine.com/questions/222353/find-path-to-location-synchronously-not-working-on.html