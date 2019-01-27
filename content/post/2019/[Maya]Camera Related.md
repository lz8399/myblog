+++
title= "[Maya]Camera Related"
date= "2019-01-27T21:52:40+08:00"
categories= ["Maya"]
tags= ["Modeling"]
thumbnailImage= "/thumbnail/cover-seattle-002.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++

##### How display an extreme large (too huge) object
<!--more-->
Problem:  
If an object is too huge, you can't see it in viewport event you scroll mouse wheel on and on.

Solution:  
open viewport menu: View -> Select Camera
{{< figure src="/img/20190127-[Maya]Camera Related/[Maya]Camera Related-01.jpg">}}

open Tab `perspShape`, modify `Far Clip Plane` (default is 10000.f)
{{< figure src="/img/20190127-[Maya]Camera Related/[Maya]Camera Related-02.jpg">}}

Effect:
{{< figure src="/img/20190127-[Maya]Camera Related/[Maya]Camera Related-03.jpg">}}


***
`世界只有一个，就是此刻压迫着你的这个，你也只在这一分钟活着，就是此刻这一分钟；而唯一的生命之道，就是接纳每一分钟，视之为独一无二的奇迹。`
