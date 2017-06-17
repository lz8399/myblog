---
title: "[UE4]UserWidge的C++常用父类函数"
date: "2017-05-31T14:13:40+08:00"
categories:
- UnrealEngine4
tags:
- UE4
---

如果要在widget的C++代码中处理初始化逻辑（比如获取获取某个button对象），建议在NativeConstruct中操作，因为Initialize()需要判定Super::Initialize()的返回值是否为true，如果为false，无法获取内部组件。

    virtual bool Initialize();

    virtual void NativePreConstruct();
	virtual void NativeConstruct();
	virtual void NativeDestruct();

	virtual void NativeTick(const FGeometry& MyGeometry, float InDeltaTime);
	virtual void NativePaint( FPaintContext& InContext ) const;

	virtual bool NativeIsInteractable() const;
	virtual bool NativeSupportsKeyboardFocus() const;