---
title: "[UE4]转载：内存管理 – 实践"
date: "2017-04-26T14:11:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

原文：http://blog.csdn.net/yangxuan0261/article/details/52075581

#### UObject gc机制

* 通过 UPROPERTY() 去保持引用

        UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "MyChar")
        class UBehavData* mBehavData;

        mBehavData = NewObject<UBehavData>(this, UBehavData::StaticClass());
        bh->mId = 111;
        
* TArray保持引用如果有个 TArray 容器，则这个TArray需要用一个* UPROPERTY()* 去保持容器的引用，然后里面的UObject就不需要再去AddToRoot去阻止被gc了。

        UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "UCoolDownComponent")
        TArray<UCoolDown*>      mCDArr;

        UCoolDown* cd = NewObject<UCoolDown>(_class);
        cd->SetSkillId(_skillId);
        mCDArr.Add(cd);
    
    容器clear后，元素会自动被gc
    
* 4.15版本支持了蓝图 TMap 容器，也是可以通过 UPROPERTY()去保持容器的引用，容器内的UObject就不需要再去AddToRoot去阻止被gc了

        UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "MyChar")
            TMap<int32, UBehavData*> mTestMap2;

        UBehavData* bh = NewObject<UBehavData>(this, UBehavData::StaticClass());
        bh->mId = 111;
        mTestMap2.Add(111, bh);
        bh = NewObject<UBehavData>(this, UBehavData::StaticClass());
        bh->mId = 222;
        mTestMap2.Add(222, bh);
        

* 没有任何容器保持引用需要AddToRoot添加标记去阻止被gc
        
        m_sInstance = NewObject<T>();
        m_sInstance->AddToRoot();
        
    让对象重新被gc回收，需要移除标记（不是立即释放对象，是在某个时间gc时才释放对象）
    
        m_sInstance->RemoveFromRoot();
        m_sInstance = nullptr;
        
* c++ new对象丢个蓝图引用住防止gc

    c++ new对象
    
        UFUNCTION(BlueprintPure, Category = "UBehavData")
        static UBehavData* CreateBehavData();

        UBehavData * UBehavData::CreateBehavData()
        {
            UBehavData* behavData = (UBehavData*)NewObject<UBehavData>(UBehavData::StaticClass());
            return behavData;
        }

    蓝图 第一时间 用一个变量 mBehavData 引用住，就可以防止这个对象被gc掉。切记第一时间。
    {{< figure src="/img/20170426-[UE4]内存管理 – 实践/[UE4]内存管理 – 实践-01.jpg">}}
    
    将蓝图中的变量 mBehavData 设为 null，则对象会被gc不定时回收掉 
    {{< figure src="/img/20170426-[UE4]内存管理 – 实践/[UE4]内存管理 – 实践-02.jpg">}}

* 强制gc

        GWorld->GetWorld()->ForceGarbageCollection(true);
        
        
#### AActor gc机制

一般重写这两个函数，来做一些初始化和清理工作

    virtual void PostActorCreated() override; //做初始化工作
    virtual void BeginPlay() override; //做初始化工作
    virtual void BeginDestroy() override; //引擎在gc的时候调用，并不是立即调用，一般不用
    virtual void EndPlay(const EEndPlayReason::Type EndPlayReason) override; //做清理工作
    virtual void Destroyed() override; //用于释放成员，调用Destroy();会立即调用
    
调用SpawnActor或DestroyActor会调用到这两个函数，析构函数则要在gc的时候才会调用，可以调用gc函数测试一下

    GWorld->GetWorld()->ForceGarbageCollection(true);

#### UActorComponent gc机制

* 作为Actor的组件存在于Actor的组件列表中，销毁Actor时会把组件列表遍历一边destroy掉并标记为待gc的对象，在一个不定时的时间被gc掉

        UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "MyChar")
        UCoolDownComponent*     mCDComp;    //注册cd组件
        
* 任意时刻销毁，即使宿主Actor未被销毁C++销毁则直接调用接口

        void UActorComponent::DestroyComponent(bool bPromoteChildren/*= false*/)

    蓝图销毁，需要设置一个UActorComponent的属性
        
            bAllowAnyoneToDestroyMe = true;
            
    因为提供给蓝图的接口需要判断这个字段，默认是false
        
        UFUNCTION(BlueprintCallable, Category="Components", meta=(Keywords = "Delete", HidePin="Object", DefaultToSelf="Object", DisplayName = "DestroyComponent"))
        void K2_DestroyComponent(UObject* Object);

        void UActorComponent::K2_DestroyComponent(UObject* Object)
        {
            AActor* MyOwner = GetOwner();
            if (bAllowAnyoneToDestroyMe || Object == this || MyOwner == NULL || MyOwner == Object)
            {
                DestroyComponent();
            }
            else
            {
                // TODO: Put in Message Log
                UE_LOG(LogActorComponent, Error, TEXT("May not destroy component %s owned by %s."), *GetFullName(), *MyOwner->GetFullName());
            }
        }
            
* 一般重写这两个函数，来做一些初始化和清理工作

        // Begin UActorComponent Interface.
        virtual void BeginPlay() override; //组件RegisterComponent注册的时候，且有OwnerActor才会立即调用，一般不用
        virtual void BeginDestroy() override; //引擎在gc的时候调用，并不是立即调用，一般不用
        virtual void EndPlay(const EEndPlayReason::Type EndPlayReason) override; //立即调用，一般这里做清理工作（注册过才会调用），且gc时还会再调用一次，一般不用
        virtual void OnComponentCreated() override; //组件RegisterComponent注册的时候立即调用，一般这里做初始化工作
        virtual void OnComponentDestroyed(bool bDestroyingHierarchy) override;//立即调用，一般这里做清理工作（只要DestroyComponent就会调用）

        // End UActorComponent Interface.
    
    默认的gc是时间测试得到为1min
    如果需要立即销毁，使用这个接口 
        
        mCDComp->DestroyComponent(); //会立即调用到 OnComponentDestroyed，并标记为准备被gc回收

        
#### 参考资料
官网地址： https://wiki.unrealengine.com/Garbage_Collection_%26_Dynamic_Memory_Allocation