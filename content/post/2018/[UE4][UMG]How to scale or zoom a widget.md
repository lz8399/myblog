+++
title= "[UE4][UMG]How to scale or zoom a widget"
date= "2018-12-01T02:09:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "UMG", "zoom"]
+++

Have a widget with Parent Canvas and a Panning Canvas nested inside:

+ set Parent Canvas to Visible
+ set Panning Canvas to Self Hit Test Invisible
+ make the Panning Canvas significantly larger than the Parent Canvas
+ place widgets in the Panning Canvas

We'll be shifting the Panning Canvas inside the Parent Canvas.

+ have a bool canPan controlled by the overridden onMouseDown/Up
+ override onMouseMove branched by the above bool and do the following while True:
+ Panning Canvas as Canvas Slot.Get Position + Get Cursor Delta -> Set Panning Canvas Position

For Mouse Zoom:

+ override onMouseWheel
+ add Wheel Delta to Panning Canvas' Render Transform Scale
+ clamp min result to something above 0 (widgets flip if scaled below 0) and max to your desired max zoom
+ Set Render Scale of the Panning Canvas with the result of the above

That should be it. You will need to work in handled / unhandled returns into the overridden functions if you want to be able to tunnel through correctly to other widgets - may not be necessary, depending on how complex this is going to be.

edit: forgot to add one thing about zooming, you will need to shift the canvas while zooming to emulate zooming into the cursor position - the above setup would only zoom in to the screen centre.

Reference: How to scale/zoom a widget with blueprints?  
https://answers.unrealengine.com/questions/815202/how-to-scalezoom-a-widget-with-blueprints.html