+++
title= "[Math]Check if a point is inside regular hexagon"
date= "2019-02-25T18:12:02+08:00"
categories= ["Math"]
tags= ["Math"]
thumbnailImagePosition= "left"
thumbnailImage= "/thumbnail/thumbnail-japen-010.jpg"
+++

Keywords: 计算坐标点是否在六边形内部
<!--more-->

Diagram

{{< figure src="/img/20190225-[Math]Check if a point is inside regular hexagon/[Math]Check if a point is inside regular hexagon-01.png">}}
	
code:
	
	boolean IsInsideHexagon(float hX, float hY, float d, float pX, float pY) 
	{
		float dx = Math.abs(pX - hX) / d;
		float dy = Math.abs(pY - hY) / d;
		float a = 0.25 * Math.sqrt(3.0);
		return (dy <= a) && (a * dx + 0.25 * dy <= 0.5 * a);
	}
	
Explaination

+ `dy <= a` checks that the point is below the horizontal edge.
+ `a * dx + 0.25 * dy <= 0.5 * a` checks that the point is to the left of the sloped right edge.
+ For `{hX = 0, hY = 0, d = 1}`, the corner points would be `(±0.25, ±0.43)` and `(±0.5, 0.0)`.
	
Reference: Is a point inside regular hexagon  
https://stackoverflow.com/a/5195868/1645289

***
`经历过孤独的日子，我终于喜欢上自己的无知，与它们相处感到惬意，如同它是一炉旺火。这时就该听任火焰的缓缓燃烧，不说一句话表示自己对无论何事的看法。必须在无知中自我更新。——玛格丽特·杜拉斯（MargueriteDuras）`
