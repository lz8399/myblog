+++
title= "[UE4]Editor Extention Related"
date= "2018-12-06T17:39:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Editor", "C++", "Module"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-013.jpg"
+++

Easy example of How to create menus in the editor  
Customizing the editor's toolbar buttons menu via custom plugin  

<!--more-->

UE4 - Easy example of How to create menus in the editor  
http://www.danielmayor.com/ue4-simple-menus

UE4 Level Editor  
https://books.google.com.sg/books?id=zZ7cDgAAQBAJ&pg=PA272&lpg=PA272&dq=UE4+leveleditor+C%2B%2B&source=bl&ots=ZsX7ZCR6bV&sig=6_J7xzxTDosX5dOuLwpiaKrOSHU&hl=zh-CN&sa=X&ved=2ahUKEwji8aiT8orfAhWFTn0KHU0JB7wQ6AEwBXoECAUQAQ#v=onepage&q=UE4%20leveleditor%20C%2B%2B&f=false

Creating an Editor Module  
https://wiki.unrealengine.com/Creating_an_Editor_Module

Customizing the editor's toolbar buttons menu via custom plugin  
https://answers.unrealengine.com/questions/25609/customizing-the-editors-toolbar-buttons-menu-via-c.html

UE4 Editor Toolbar Extention  
https://blog.csdn.net/hui211314ddhui/article/details/79375548

##### Editor Programming Related

Properties changed event

	#if WITH_EDITOR
	virtual void PostEditChangeProperty(FPropertyChangedEvent& PropertyChangedEvent) override;
	#endif

Actor moved event

	#if WITH_EDITOR
	/** Called after an actor has been moved in the editor */
	virtual void PostEditMove(bool bFinished);
	#endif

***
`因为太爱一个人，所以不敢做真实的自己，反而越容易分手。`