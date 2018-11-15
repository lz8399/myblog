+++
title= "[UE4]Destructible Mesh Workflow"
date= "2018-11-14T16:20:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4"]
+++

Take damage, destruct mesh if damage is enough:

    // Take damage
	UFUNCTION(BlueprintCallable, Category="Components|Destructible")
	virtual void UDestructibleComponent::ApplyDamage(float DamageAmount, const FVector& HitLocation, const FVector& ImpulseDir, float ImpulseStrength) override;

	// Take radius damage
	UFUNCTION(BlueprintCallable, Category="Components|Destructible")
	virtual void UDestructibleComponent::ApplyRadiusDamage(float BaseDamage, const FVector& HurtOrigin, float DamageRadius, float ImpulseStrength, bool bFullDamage) override;