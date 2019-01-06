+++
title= "[UE4]Hardware cursor(solution for UMG customized cursor lagging)"
date= "2018-12-17T12:05:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UMG", "cursor", "lagged"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-010.jpg"
+++

Put a PNG in game content directory

<!--more-->

Steps

1, Put a PNG in game content directory, e.g. `E:\MyProj\Content\Asset\Cursor\mouse.png`

2, Project Settings -> Engine -> User Interface -> Hardware Cursors -> add element and set `Default`, set `Cursor Path` as `Asset/Cursor/mouse`.

3, If the click response position of .PNG cursor isn't the top-left corner, you can modify the `Hot Spot`, e.g. you can set Hot Spot as (0.5, 0.5) if the click response position is the center of .PNG.
