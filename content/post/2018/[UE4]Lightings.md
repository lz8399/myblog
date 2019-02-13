+++
title= "[UE4]Lightings"
date= "2018-04-27T14:14:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Lightings"]
+++

keywords：UE4、Lighting、灯光

以下问题都是基于4.18，不排除后续新版本变动。

##### Lighting Content Examples

https://docs.unrealengine.com/en-us/Resources/ContentExamples/Lighting


##### Light Propagation Volumes
Light Propagation Volumes  
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/LightPropagationVolumes

Dynamic GI : Getting the Most out of LPV ( Light Propagation Volume )  
https://forums.unrealengine.com/community/community-content-tools-and-tutorials/103572-dynamic-gi-getting-the-most-out-of-lpv-light-propagation-volume

##### Lighting Channels
https://docs.unrealengine.com/en-us/Engine/Rendering/LightingAndShadows/LightingChannels

实际应用：  
假设场景中只有一个平行光，且光照强度较大时，那么角色身上接收不到直接光照的部位（比如脖子），会明显发黑，如果增大 SkyBox 光照强度，那么会影响整个场景的亮度。有没办法只增加角色身上的光照亮度？让阴影区域变亮？解决办法是：Lighting Channels。  
解决办法：  
场景中添加两个平行光，A平行光的 Lighting Channels 只开启Channel 0，B平行光只开启Channel 1，然后角色的 Mesh 同时开启 Channel 0 和 Channel 1。


注意事项：

+ Lighting Channels是动态的，意思是：静态光(Static Lights)或者Mobility为Static的Static Mesh Actor不受Lighting Channels影响。要使用Lighting Channels，Static Mesh Actor和Lights的Mobility必须设置为Stationary或者Movable。
+ 材质类型影响：Lighting Channels只影响直接光照(direct lighting)下Opaque类型材质，Translucent或者Masked类型材质没有效果。
+ Lighting Channels对性能开销不大，可以忽略不计。

移动端的Lighting Channels：

+ 4.13版本开始，才支持移动端的Lighting Channel。
+ 移动端多个Directional Light支持不同Lighting Channels。
+ 一个Primitives只受一个Directional Light影响，如果primitves勾选了多个Lighting Channel，那么只会启用第一个。
+ CSM Shadows只会投射到与光源Lighting Channels相同的primitives上。
+ 动态点光源在移动端支持Lighting Channels的所有特性，与桌面级特性相同。

另外：Lighting Channels不支持运行时修改，就是说Lighting Channels在Actor创建时(比如BeginPlay)设置好以后，之后就无法再修改。

##### Occlusion Culling 光源距离裁剪
Project Settings -》 Engine -》 Rendering -》 Culling -》 Min Screen Radius for Lights  

Lights view distance  
https://forums.unrealengine.com/unreal-engine/feedback-for-epic/54065-lights-view-distance


##### Lighting Related on Mobile

1，`Static` and `Stationary` Spotlight support on Mobile, but `Movable` Spotlight not support on Mobile before v4.22;

2, `Movable` Pointlight support on Mobile always;

##### 物体与摄像机距离超过一定范围时，阴影自动消失的问题

这个问题受两个因素影响：

1，DirectionalLight 的属性 `Dynamic Shadow Distance`，如果值小于物体到摄像机的直线距离，则阴影消失。

2，引擎配置参数 `r.Shadow.RadiusThreshold`，表示在屏幕中大小的屏占比 ，该值受 Settings -》 Engine Scalability Settings -》 Shadow 级别控制。

参考：  
https://answers.unrealengine.com/questions/707241/object-shadows-disappearing-too-early.html?sort=oldest
	
### LightComponentBase (the basic of LightComponent)

##### LightComponentBase's API in common

Properties:

	/** 
	 * Total energy that the light emits.  
	 */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(DisplayName = "Intensity", UIMin = "0.0", UIMax = "20.0"))
	float Intensity;

	/** 
	 * Filter color of the light.
	 * Note that this can change the light's effective intensity.
	 */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(HideAlphaChannel))
	FColor LightColor;

	/** 
	 * Whether the light can affect the world, or whether it is disabled.
	 * A disabled light will not contribute to the scene in any way.  This setting cannot be changed at runtime and unbuilds lighting when changed.
	 * Setting this to false has the same effect as deleting the light, so it is useful for non-destructive experiments.
	 */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Light)
	uint32 bAffectsWorld:1;

	/**
	 * Whether the light should cast any shadows.
	 **/
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Light)
	uint32 CastShadows:1;

	/**
	 * Whether the light should cast shadows from static objects.  Also requires Cast Shadows to be set to True.
	 */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Light, AdvancedDisplay)
	uint32 CastStaticShadows:1;

	/**
	 * Whether the light should cast shadows from dynamic objects.  Also requires Cast Shadows to be set to True.
	 **/
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Light, AdvancedDisplay)
	uint32 CastDynamicShadows:1;

	/** Whether the light affects translucency or not.  Disabling this can save GPU time when there are many small lights. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=Light, AdvancedDisplay)
	uint32 bAffectTranslucentLighting:1;

	/** Whether light from this light transmits through surfaces with subsurface scattering profiles. Requires light to be movable. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Light, AdvancedDisplay)
	uint32 bTransmission : 1;

	/** Whether the light shadows volumetric fog.  Disabling this can save GPU time. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Light, AdvancedDisplay)
	uint32 bCastVolumetricShadow : 1;

	/** 
	 * Scales the indirect lighting contribution from this light. 
	 * A value of 0 disables any GI from this light. Default is 1.
	 */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(UIMin = "0.0", UIMax = "6.0"))
	float IndirectLightingIntensity;

	/** Intensity of the volumetric scattering from this light.  This scales Intensity and LightColor. */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(UIMin = "0.25", UIMax = "4.0"))
	float VolumetricScatteringIntensity;
	
### LightComponent (the basic component of various Light)

Engine\Source\Runtime\Engine\Classes\Components\LightComponent.h

##### LightComponent's API in common

Properties:

	/** 
	 * Whether to render light shaft bloom from this light. 
	 * For directional lights, the color around the light direction will be blurred radially and added back to the scene.
	 * for point lights, the color on pixels closer than the light's SourceRadius will be blurred radially and added back to the scene.
	 */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=LightShafts, meta=(DisplayName = "Light Shaft Bloom"))
	uint32 bEnableLightShaftBloom:1;

	/** Scales the additive color. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=LightShafts, meta=(UIMin = "0", UIMax = "10"))
	float BloomScale;

	/** Scene color must be larger than this to create bloom in the light shafts. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=LightShafts, meta=(UIMin = "0", UIMax = "4"))
	float BloomThreshold;

	/** Multiplies against scene color to create the bloom color. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category=LightShafts)
	FColor BloomTint;

### Sky Light

Engine\Source\Runtime\Engine\Classes\Components\SkyLightComponent.h

##### Sky Light's API in common

Properties:

	/** Whether the light shadows volumetric fog.  Disabling this can save GPU time. */
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Light, AdvancedDisplay)
	uint32 bCastVolumetricShadow : 1;

	/** 
	 * Scales the indirect lighting contribution from this light. 
	 * A value of 0 disables any GI from this light. Default is 1.
	 */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(UIMin = "0.0", UIMax = "6.0"))
	float IndirectLightingIntensity;

	/** Intensity of the volumetric scattering from this light.  This scales Intensity and LightColor. */
	UPROPERTY(BlueprintReadOnly, interp, Category=Light, meta=(UIMin = "0.25", UIMax = "4.0"))
	float VolumetricScatteringIntensity;
	
Functions:

	/** Sets the cubemap used when SourceType is set to SpecifiedCubemap, and causes a skylight update on the next tick. */
	UFUNCTION(BlueprintCallable, Category="SkyLight")
	void SetCubemap(UTextureCube* NewCubemap);

	/** 
	 * Creates sky lighting from a blend between two cubemaps, which is only valid when SourceType is set to SpecifiedCubemap. 
	 * This can be used to seamlessly transition sky lighting between different times of day.
	 * The caller should continue to update the blend until BlendFraction is 0 or 1 to reduce rendering cost.
	 * The caller is responsible for avoiding pops due to changing the source or destination.
	 */
	UFUNCTION(BlueprintCallable, Category="SkyLight")
	void SetCubemapBlend(UTextureCube* SourceCubemap, UTextureCube* DestinationCubemap, float InBlendFraction);
	
	/** Indicates that the capture needs to recapture the scene, adds it to the recapture queue. */
	void SetCaptureIsDirty();
	void SetBlendDestinationCaptureIsDirty();
	void SanitizeCubemapSize();

	/** Whether sky occlusion is supported by current feature level */
	bool IsOcclusionSupported() const;

	/** 
	 * Recaptures the scene for the skylight. 
	 * This is useful for making sure the sky light is up to date after changing something in the world that it would capture.
	 * Warning: this is very costly and will definitely cause a hitch.
	 */
	UFUNCTION(BlueprintCallable, Category="Rendering|Components|SkyLight")
	void RecaptureSky();
	
	
### Exponential Height Fog

Engine\Source\Runtime\Engine\Classes\Components\ExponentialHeightFogComponent.h

##### Exponential Height Fog's API in common

Properties:

	/** Global density factor. */
	UPROPERTY(BlueprintReadOnly, interp, Category=ExponentialHeightFogComponent, meta=(UIMin = "0", UIMax = ".05"))
	float FogDensity;

	UPROPERTY(BlueprintReadOnly, interp, Category=ExponentialHeightFogComponent)
	FLinearColor FogInscatteringColor;
	
	/** 
	 * Controls the color of the directional inscattering, which is used to approximate inscattering from a directional light. 
	 * Note: there must be a directional light with bUsedAsAtmosphereSunLight enabled for DirectionalInscattering to be used.
	 */
	UPROPERTY(BlueprintReadOnly, interp, Category=DirectionalInscattering)
	FLinearColor DirectionalInscatteringColor;

##### Reference
Lighting Passes  
https://unrealartoptimization.github.io/book/profiling/passes-lighting/

***
`我只担心一件事，我怕我配不上自己所受的苦难。----陀思妥耶夫斯基`