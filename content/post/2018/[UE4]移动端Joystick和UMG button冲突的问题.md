+++
title= "[UE4]移动端Joystick和UMG button冲突的问题"
date= "2018-01-14T16:10:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Joystick", "UMG", "Button", "Conflict"]
+++

问题1：UMG widget 遮挡 joystick，导致joystick只显示无法使用的问题。  
原因：UMG的Canvas Panel组件的Visibility属性被修改了。  
解决办法：打开UMG蓝图，设置Canvas Panel的Visibility为：Self Hit Test Invisible。

问题2：joystick摇杆和UMG button在移动端冲突的问题：按住摇杆时，UMG button按了不起作用。  
原因：UMG button的Is Focusable属性设置为了true。  
解决办法：UMG button的Is Focusable属性设置为false。

问题3：Widget的Visibility属性默认为Self Hit Test Invisible，这样，每当有新的Widget AddToViewport时，当前Widget会被自动隐藏。但是默认的Visibility无法响应Widget之外的鼠标或touch事件（比如一个UButton，如果按住UButton不放，然后鼠标或者手指拖拽到UButton之外，那么当松开鼠标或手指时，该button的Release事件无法响应），但是Visibility属性如果设置成Visible，那么就可以相应，但是当新的Widget添加Viewport时，当前Widget不会自动隐藏。

参考：Virtual Joystick conflicts UMG Buttons  
https://answers.unrealengine.com/questions/211064/virtual-joystick-conflicts-umg-buttons.html

***
`念念不忘，必有回响。----陈念萱`