+++
title= "[UE4]Renderer Related"
date= "2019-01-25T18:32:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Rendering"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-005.jpg"
+++

##### How to enable "Forward Rendering"

<!--more-->

Project Settings -> Rendering -> "Forward Shading" Checkbox (now you can use that silky MSAA)
{{< alert success >}}
Default Rendering Mode is Deferred Shading.
{{< /alert >}}

##### How to enable fogging on mobile

Project Settings -> Engine -> Rendering -> Mobile -> Uncheck `Disable vertex fogging in mobile shaders`

##### Reference

Rendering Overview  
https://docs.unrealengine.com/en-us/Engine/Rendering/Overview

Forward vs Deferred Shading  
https://unrealartoptimization.github.io/book/pipelines/forward-vs-deferred


***
`我要在最细的雨中`  
`吹出银色的花纹`  
`让所有在场的丁香`  
`都成为你的伴娘`  
`我要张开梧桐的手掌`  
`去接雨水洗脸`  
`让水杉用软弱的笔尖`  
`在风中写下誓言`  
`——顾城`
