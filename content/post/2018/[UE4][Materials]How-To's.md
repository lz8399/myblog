+++
title= "[UE4][Materials]How-To's"
date= "2018-12-22T22:41:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4"]
keywords= ["UE4", "Materials", "metal part"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-004.jpg"
+++

How to metal only for a part of mesh  
How to make a stained glass window effect  

<!--more-->

### UE4 Materials How-To's

https://docs.unrealengine.com/en-us/Engine/Rendering/Materials/HowTo


##### How to metal only for a part of mesh

Using Texture Masks  
https://docs.unrealengine.com/en-us/Engine/Rendering/Materials/HowTo/Masking

##### How to make a stained glass window effect

Using Colored Translucent Shadows  
https://docs.unrealengine.com/en-us/Engine/Rendering/Materials/HowTo/ColoredTransluscentShadows

##### How to create a richly colored metallic surface

Create a richly colored metallic surface in UE4  
https://odederell3d.wordpress.com/2018/02/08/create-a-richly-colored-metallic-surface-in-ue4/

##### How To Use The Spiral Blur Material Node

How To Use The Spiral Blur Material Node  
https://wiki.unrealengine.com/How_To_Use_The_Spiral_Blur_Material_Node

##### Font Materials and Outlines

Font Materials and Outlines  
https://docs.unrealengine.com/en-us/Engine/UMG/UserGuide/Fonts/Materials

##### How to clip material in circle range

How can I make a 2D Material into a circle? ( circle range clip )  
https://answers.unrealengine.com/questions/565198/how-can-i-make-a-2d-material-into-a-circle.html

Make a square material into a circle  
https://answers.unrealengine.com/questions/717609/make-a-square-material-into-a-circle.html

##### How to manipulate texture repeat, uv on a material

Create a new material, with a Texture2D, or a Texture2D Parameter, difference being a paramater can be changed outside of the material editor!

There is an input UV on the Texture2D with UV on it. You can connect this with a TexCoord, but this texcoord is not a parameter, so can't be changed outside of the material....

UV's are values between 0 and 1. If it's more than 1, it will repeat itself. So to make sure we can change it we need a so called Scalar Parameter. Give the scalar parameter a name to your liking, i.e. "UV Tiling". Now multiply this value with TexCoord. Now Connect the multiply with the UV's from the Texture2D node. Compile/Save.

Now in the Content Browser you need to make an instance. Because we can't change a material directly, but we can change a material instance. Right click on the material and select "Create Instance". Give it a cool name and put it on the object.

If you go into the material instance you will see your Scalar Parameter "UV Tiling". You can change it by enabling it first with the toggle next. Change the value to see if it is actually tiling the way you want to.

Now you can change this parameter in Blueprint. Not really sure what the blueprint nodes are named exactly (currently not sitting behind my UE4 computer.). But if you look for material, or parameter you might find something you are looking for.

So remember: The object that you are changing should have the INSTANCE applied!

Side node: If you want different x and y tiling, you can append 2 Scalar Parameters together and multiply that with the TexCoord node.

Reference   
https://answers.unrealengine.com/questions/17303/how-to-manipulate-texture-repeat-uv-on-a-material.html

##### How to set UV Coordinate offset of Texture and zoom in / out it

{{< figure src="/img/20181222-[UE4][Materials]How-To's/[UE4][Materials]How-To's-01.jpg">}}

Can texture coordinate parameters be applied to material instances?  
https://answers.unrealengine.com/questions/19412/can-texture-coordinate-parameters-be-applied-to-ma.html


##### Dissolve Effect
Dissolve effects in UE4  
http://martiancraft.com/blog/2015/02/disintegrating-baddies/

Planar Dissolve Effect - Material Tutorial - (Unreal Engine 4)  
https://www.youtube.com/watch?v=HR3flKges_A

***
`渐渐的知道了，很多东西可遇而不可求，不属于自己的，何必拼了命去在乎，你在意什么，什么就会折磨你，期待是所有心痛的根源。`