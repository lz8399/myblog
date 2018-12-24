---
title: "[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)"
date: "2016-11-27T22:20:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
- Material
---

#### 蓝图方式：


使用StarterContent中的椅子作为演示示例的模型：

1，	创建一个空的Actor蓝图，命名为RandomChair：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-01.jpg">}} 

2，打开蓝图
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-02.jpg">}}  

并将椅子的StaticMesh拖放的到根节点内：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-03.jpg">}}  

{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-04.jpg">}} 

3，在该蓝图内创建一个box，命名为Box1，用于检测碰撞时使用：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-05.jpg">}} 

4，将这个蓝图拖放到场景中：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-06.jpg">}}  

5，添加蓝图脚本

现在构造函数中创建一个材质示例，并命名为DynamicMetarial
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-07.jpg">}} 

{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-08.jpg">}}  

然后再添加Box1的碰撞事件函数

{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-09.jpg">}} 

{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-10.jpg">}} 

全部逻辑为：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-11.jpg">}} 
 
每当靠近这个椅子时，椅子的颜色就会随机变化一次。

其中的参数名：ColorSeats，是在Chair的材质中定义的可编辑参数：
{{< figure src="/img/20161127-[UE4][Material]使用蓝图和C++动态创建材质并设置材质参数属性(Parameter)/[UE4][Material]动态创建材质并设置材质参数属性(Parameter)-12.jpg">}}  

#### C++方式：

加载材质并为 Image 空间设置材质资源

	UMaterial* Mat = LoadObject<UMaterial>(nullptr, TEXT("Material'/Game/Asset/Materials/HUD/ProgressCircleRotate/M_ProgressCircleRot.M_ProgressCircleRot'"));
	if (Mat && Img)
	{
		if (UMaterialInstanceDynamic* MatInstance = UMaterialInstanceDynamic::Create(Mat, this))
		{
			Img->SetBrushFromMaterial(MatInstance);
		}
	}

设置动态参数
	
	if (Img)
		{
			if (UMaterialInstanceDynamic* MatInsDyna= Cast<UMaterialInstanceDynamic>(Img->Brush.GetResourceObject()))
			{
				MatInsDyna->SetScalarParameterValue("Alpha", 0.8);
			}
		}

设置动态参数的其他接口（MaterialInstanceDynamic.h）


    void SetVectorParameterValue(FName ParameterName, FLinearColor Value);
    
    bool SetScalarParameterValue(FName ParameterName,, float Value);
    
    void SetTextureParameterValue(FName ParameterName, class UTexture* Value);
    
    void SetFontParameterValue(const FMaterialParameterInfo& ParameterInfo, class UFont* FontValue, int32 FontPage);
    
    void ClearParameterValuesInternal();
