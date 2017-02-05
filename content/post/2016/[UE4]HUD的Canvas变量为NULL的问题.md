---
title: "[UE4]HUD的Canvas变量为NULL的问题"
date: "2016-10-24T23:06:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

AHUD中的成员变量Canvas只在PostRender()事件中有效，离开此函数后就会被引擎置空。
要想使用HUD的Canvas，必须重写HUD的两个函数之一：

    /** PostRender is the main draw loop. */
    virtual void PostRenderFor();

    /** The Main Draw loop for the hud.  Gets called before any messaging.  Should be subclassed */
    virtual void DrawHUD();

其中DrawHUD为HUD独有的函数，而PostRender是所有Actor都有函数。
另外注意：**PostRenderFor()不是重写了就会触发**，还需要执行`AHUD::AddPostRenderedActor()`，将需要触发的Actor加入PostRenderActors数组中。


Canvas的引擎源码注释：

    protected:
        /** Canvas to Draw HUD on.  Only valid during PostRender() event.  */
        UPROPERTY()
        UCanvas* Canvas;


