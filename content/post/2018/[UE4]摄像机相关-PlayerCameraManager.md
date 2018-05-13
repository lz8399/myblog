+++
title= "[UE4]摄像机相关-PlayerCameraManager"
date= "2018-01-12T14:55:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "PlayerCameraManager"]
+++

##### 设置默认的PlayerCameraManager
PlayerController构造函数中设置PlayerCameraManagerClass：

	PlayerCameraManagerClass = AMyPlayerCameraManager::StaticClass();

##### 摄像机不跟随角色一起旋转

	USpringArmComponent::bAbsoluteRotation = true;
	
***
`养老江湖外，藏名诗画中。----白狼`