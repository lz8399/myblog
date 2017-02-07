---
title: "[Maya][Material]3S贴图制作皮肤"
date: "2016-12-11T17:26:40+08:00"
categories:
- Maya
tags:
- Material
---

转载：http://jingyan.baidu.com/article/0320e2c1ec5a631b87507bb1.html

3s材质球贴图，可以让对应目标物体显示出更加真实的效果，一般应用于人物模型制作中。3s贴图一般包括有人物的表皮层，真皮层，和中间层。另外，为了模型的真实度，还有涉及到法线贴图，高光贴图等。
1、首先，要让材质库存在3s贴图，必须要打开maya mental ray的选项。所以，依次打开window--setting/preferences--plug-in   manager，找到mayatomr.mll这个选项，2014版本以前的在上面显示，2014版本的maya在下面中间显示（不要看掉了哦）。勾选后面的loaded,Maya就会自动加载Mental ray 渲染器了。如果要每次启动Maya，都自动加载Mental ray ，只要把后面的auto load构选上即可。
{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-01.jpg">}}
 
2、然后再在window---rendering   editors---hypershade（打开材质球）中找到mental  ray里面的misss_fast_skin_maya这个选项，即是真人皮肤的3s贴图材质球。
{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-02.jpg">}}
 
下面介绍下3s材质球的一些属性。
{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-03.jpg">}}

{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-04.jpg">}}

{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-05.jpg">}}

{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-06.jpg">}}

{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-07.jpg">}}

{{< figure src="/img/20161211-[Maya][Material]3S贴图制作皮肤/[Maya][Material]3S贴图制作皮肤-08.jpg">}}
 
 
 
 
 
 

