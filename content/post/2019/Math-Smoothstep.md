+++
title= "Math-Smoothstep"
date= "2019-03-20T18:12:02+08:00"
categories= ["Math"]
tags= ["Math"]
mathjax= ["ture"]
thumbnailImage= "/thumbnail/cover-Tso Moriri Lake.jpg"
autoThumbnailImage= "true"
thumbnailImagePosition= "top"
+++

Origin Text:  
<!--more-->
https://en.wikipedia.org/wiki/Smoothstep


**Smoothstep** is a family of sigmoid-like interpolation and clamping functions commonly used in computer graphics and video game engines.

The function depends on three parameters, the input x, the "left edge" and the "right edge", with the left edge being assumed smaller than the right edge. The function receives a real number x as an argument and returns 0 if x is less than or equal to the left edge, 1 if x is greater than or equal to the right edge, and smoothly interpolates, using a Hermite polynomial, between 0 and 1 otherwise. The slope of the smoothstep function is zero at both edges. This is convenient for creating a sequence of transitions using smoothstep to interpolate each segment as an alternative to using more sophisticated or expensive interpolation techniques.

With no salient loss of generality, the left edge may be set to 0 and the right edge to 1. Then the general form for smoothstep is

{{< figure src="/img/20190320-[Math]Smoothstep/[Math]Smoothstep-01.svg">}}

$S_0(x)$ is identical to the **clamping function**:
{{< figure src="/img/20190320-[Math]Smoothstep/[Math]Smoothstep-02.svg">}}

The characteristic "S"-shaped sigmoid curve is obtained with $S_N(x)$ only for integers N ≥ 1. The order of the polynomial in the general smoothstep is 2N + 1. With N = 1, the slopes or first derivatives of the smoothstep are equal to zero at the left and right edge (x = 0 and x = 1), where the curve is appended to the constant or saturated levels. With higher integer N, the second and higher derivatives are zero at the edges, making the polynomial functions as flat as possible and the splice to the limit values of 0 or 1 more seamless.

In HLSL and GLSL, smoothstep implements the $S_1(x)$, the cubic **Hermite interpolation** after clamping:

{{< figure src="/img/20190320-[Math]Smoothstep/[Math]Smoothstep-03.svg">}}

Again, assuming that the left edge is 0, the right edge is 1, with the transition between edges taking place where 0 ≤ x ≤ 1.

A C/C++ example implementation provided by AMD follows.

	float smoothstep(float edge0, float edge1, float x) {
	  // Scale, bias and saturate x to 0..1 range
	  x = clamp((x - edge0) / (edge1 - edge0), 0.0, 1.0); 
	  // Evaluate polynomial
	  return x * x * (3 - 2 * x);
	}

	float clamp(float x, float lowerlimit, float upperlimit) {
	  if (x < lowerlimit)
		x = lowerlimit;
	  if (x > upperlimit)
		x = upperlimit;
	  return x;
	}

***
`当前的目标并不在于发现我们是谁，而是拒绝我们是谁。——米歇尔·福柯（MichelFoucault）`
