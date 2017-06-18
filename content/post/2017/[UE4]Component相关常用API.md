---
title: "[UE4]Component相关常用API"
date: "2017-02-07T14:06:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

Actor.h

    //获取第一个与指定类型相同的Component
    UActorComponent* AActor::FindComponentByClass(const TSubclassOf<UActorComponent> ComponentClass) const

    //获取当前actor的所有component
    template<class T, class AllocatorType>
        void GetComponents(TArray<T*, AllocatorType>& OutComponents, bool bIncludeFromChildActors = false) const

    //与FindComponentByClass作用相同，暴露给蓝图使用的C++函数
    UActorComponent* AActor::GetComponentByClass(TSubclassOf<UActorComponent> ComponentClass) const

    //获取指定类型的所有Component
    TArray<UActorComponent*> AActor::GetComponentsByClass(TSubclassOf<UActorComponent> ComponentClass) const

PrimitiveComponent.h
    
    //获取当前component中材质的个数
    int32 UPrimitiveComponent::GetNumMaterials() const

    //创建一个材质对象，并替换到Parent对象上的指定index的材质
    UMaterialInstanceDynamic* UPrimitiveComponent::CreateAndSetMaterialInstanceDynamicFromMaterial(int32 ElementIndex, class UMaterialInterface* Parent)
    
    