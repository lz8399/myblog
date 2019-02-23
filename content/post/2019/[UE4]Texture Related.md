+++
title= "[UE4]Texture Related"
date= "2019-02-21T21:45:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Texture"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-012.jpg"
+++

##### Is it need to make Texture LODs?
<!--more-->

UE4 automatically make mipmaps for your textures. If you import 1024 texture to engine it's automatically creates 512,256,128,64,32,16,8,4,2,1 size textures from the original texture data. These are stored as mipmaps for original texture and it cost +33% more texture memory. When texture is sampled at material, pixel shader calculates what size mipmap it should sample. This automatic mipmapping prevents aliasing and saves a lot of texture memory bandwith. There is also texture streaming feature that only loads mipmap levels that are needed for object. If object is really far a way engine does not need to load the full size texture but small version of it. Let say 64x64 texture.

Original Text: Texture Size LODs  
https://forums.unrealengine.com/development-discussion/rendering/1445698-texture-size-lods

##### Reference

Texture Streaming  
https://docs.unrealengine.com/en-us/Engine/Content/Types/Textures/Streaming
***
`极度渴望成功的人并不多，愿付非凡代价的人更少。----美团王兴`