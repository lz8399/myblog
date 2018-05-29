+++
title= "[UE4][Animation]Master Pose, Copy Pose, Mesh merge区别"
date= "2018-05-29T16:50:02+08:00"
categories= ["UnrealEngine4"]
tags= ["UE4", "Animation"]
keywords= ["UE4", "Animation"]
+++

参考自：Master pose vs copy pose vs mesh merge in UE4  
https://iluvanimation.blogspot.tw/2017/04/master-pose-vs-copy-pose-vs-mesh-merge.html


Since I get this question so often, I'm just writing quick summary for each.

When you have different parts of bodies, and you want to allow players to pick which part they want, we have multiple choices, and people are wondering what are the main differences.

Say you have head, upper body, lower body, and how do you allow them to pick and what are the differences?

##### 1. Master Pose Component

+ This is Blueprint callable action that you set `Child->SetMaseterPoseComponent(Body)`, then **Body** becomes the master of **Child**, which means **Child** will follow whatever **Body** does.
+ Behind of scene, **Child** does not have any bone transform buffer and it doesn't run any animation system even if you set AnimBP on the **Child**, and it just uses **Body's** bone transform buffer when rendered. This makes very light weight attachment system. Only component that has to run animation is **Body**, and all attachment will just use **Body's** bone transform.
+ This does not reduce render cost. You still render # of components separate (and more drawcalls if you have more sections for each), but this reduces game thread cost.
+ Limitation
    + **Child** has to have SUBSET of exact matching structure. You can't have any other extra joint or skip the joint. Since there is no bone buffer for that extra joint, that will render in the origin of the mesh.
    + You can't run any other animation or physics on the **Child**.

##### 2. Copy Pose From Mesh

+ This is anim graph node that you can use on AnimBP of the **Child**.
+ It allows you to copy from any SkeletalMeshComponent. You also want to make sure the SkeletalMeshComponent (I'll call this **Body**) you copy from ALREADY has ticked. Otherwise you're going to copy last frame's animation. To ensure this, you can just attach **Child** to the **Body**. Once you attach, it will ensure parent ticks first before child.

{{< figure src="/img/20180529-[UE4][Animation]Master Pose, Copy Pose, Mesh merge区别/[UE4][Animation]Master Pose, Copy Pose, Mesh merge区别-01.jpg">}}

+ This only copies the bones that matching, and everything else will stay on reference pose.
+ Or you can choose to play animation on top of the copied transform as illustrated above.
+ Limitation
    + If **Body** has physics on them, you'd like to make sure to run this AFTER your parent blends physics with it, which means it has to tick in Post Physics, but that means you can't have any physics on the **Child**. I did not test this but in theory, you can have the **Child** to have physics, but not both of them at the same time.
    + Of course more expensive than Master Pose because this runs animation on each Child.

##### 3. Mesh merge. 

+ Mesh merge allows you to create SkeletalMesh from multiple meshes
+ It has high initial cost of creating the SkeletalMesh
+ Rendering cost is cheap since you can only render one mesh as opposed to multiple meshes
+ Main **Body** has to contain all the animations because the merged mesh will only use the skeleton that's set, and it will has to contain all the joints you'd need to animate. Say you have extra joints for certain body parts, you still have to have all animations on the **Body**.
+ Morphtarget is not supported
+ You only run one animation on the merged mesh.

I think this sums up the main points. I hope this helps.

With recent changes(future release of 4.17), preview animation in persona with additional meshes will use Copy Pose from Mesh since that supports both Master/Copy Pose from Mesh and we care less about performance in editor than in runtime. Also you can create custom DataAsset that supports preview and you can support your custom mesh preview. Again for 4.17 but it's coming. :)

***
`千古功名一纸书,不过扬灰于尘土。---花香蘑菇《君临臣下》`
