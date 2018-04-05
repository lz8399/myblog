+++
title= "[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust"
date= "2018-01-17T18:20:02+08:00"
categories= ["Dlang"]
tags= ["Dlang"]
+++

原文：https://imgur.com/a/jQUav#xVgi2ZA

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-01.png">}}

##### Optimizing C++ takes time! (The other lines are all at the bottom)
Compilers (all on Windows):

+ VC++ 2013 x64 without (/Od) and with optimizations (/O2)
+ Go 1.7.1 amd64 without (-gcflags -N -l) and with optimizations (no flags)
+ Rust 1.12.0 MSVCx64 without (-C opt-level=0) and with optimizations (-C opt-level=2)
+ DMD32 D 2.071.2 x64 without (no flags) and with optimizations (-O)
+ Free Pascal 3.0.0 i386 without (-O-) and with optimizations (-O2)

The source codes being compiled are the same simplistically generated programs with an increasing number of functions of about 5-20 lines each.

Example function:

	int  f91362() {
		int x1 = 480;
		x1 = x1 | (f85774() ^ f77368());
		x1 = x1 & 487;
		x1 = x1 & 388;
		return f91361() & (x1 ^ 685);
	}
	
{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-02.png">}}

##### Let's look at those other lines
Removing the optimized C++ allows us to see the other languages.

Surprise: C++ without optimizations is the fastest!

A few other surprises: Rust also seems quite competitive here. D starts out comparatively slow. (Possibly spending a lot of time linking unused libraries?)

And strangest of all: Disabling optimizations in D, Pascal, Rust or Go does not seem to help speed up compilation at all.

Maybe this is too easy. Let's try going 10x larger.

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-03.png">}}

##### 100-1000 functions: Rust slows down
C++ (without optimizations) is still king.

Another 10x larger? OK, but I'm removing Rust for now.

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-04.png">}}

##### 1000-10'000 functions

D and Pascal seem to gain on C++. Go is losing ground.

Another 10x? OK, but let's remove the optimized versions. They don't seem to be much different anyway. Maybe add Rust back into the mix for fun.

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-05.png">}}

##### 10'000-100'000 functions
Rust is still slow. C+ is starting to slow down as well. Go is back stealing C++'s lunch.
Pascal and D dropped out of the race after 30'000 functions just when they were starting to win.
Pascal: Fatal: No memory left (There was no x64 version available of the compiler.) :(
D: Error: more than 32767 symbols in object file :(

Let's kick Rust out again and zoom in on the bottom left part of this chart.

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-06.png">}}

##### 10'000-50'000 functions
Zoomed in part from the above chart shows it all:
Rust (not shown) would only just be visible on this scale.

Pascal and D are quick but not suited to the large scale, where Go overtakes C++.

{{< figure src="/img/20180117-[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust/[Dlang]Comparing compilation time of random code in C++, D, Go, Pascal and Rust-07.png">}}

##### 2'000-30'000 functions
A bit more data points to show that the lines are not as smooth as they appear above.
But the way the data was gather may be quite unrepresentative of real applications anyway, so don't take this too seriously. But maybe it can spark some interesting discussion. No pitchforks please. :)

