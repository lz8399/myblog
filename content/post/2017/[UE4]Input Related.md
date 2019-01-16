+++
title= "[UE4]Input Related"
date= "2017-12-15T14:16:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Mobile Input", "Swipe", "Pinch"]
+++

##### How to get Touch Position on screen

1. New C++ class inherit from `GameViewportClient`

2. Project Settings -> Engine -> General Settings -> Default Classes -> set `Game Viewport Client Class` as your customized class.

3. Override function `InputTouch`

		virtual bool InputTouch(FViewport* Viewport, int32 ControllerId, 
		uint32 Handle, ETouchType::Type Type, const FVector2D& TouchLocation, 
		float Force, FDateTime DeviceTimestamp, uint32 TouchpadIndex) override;
		
	Argument `TouchLocation` is the Touch Position.
	
##### Mobile Input - Swipe and Pinch

A plugin for Unreal Engine 4 that exposes touches and swipes on mobile devices as events in blueprints  
https://github.com/getsetgames/Swipe

Ultimate Touch Components  
https://www.unrealengine.com/marketplace/custom-touch-controls

***
`三十功名尘与土，八千里路云和月。----岳飞《满江红》`