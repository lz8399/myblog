+++
title= "[Dlang]D与Rust的优缺点比较"
date= "2016-05-30T09:17:02+08:00"
categories= ["Dlang"]
tags= ["Dlang", "Rust"]
+++

原文：https://users.rust-lang.org/t/rust-vs-dlang-i-want-more-experienced/4472/19

First things first:

1. You did ask this in a Rust community, so I might be biased, but I will try to be as fair as I can.
2. This of course are my personal opinions, people have different preferences so it is hard to say black-and-white that this is good and this is bad. Take it as “this might be true, I will take this into consideration and research these points and then build on that”.
3. I don’t have much experience with D. I was interested in it at some point and researched it marginally. After finding that it does not bring much more than C++ to the table(Note that C++ has taken a lot of ideas from D and this is acknowledged. That’s why it’s not a big surprise that C++ contains most of D’s features), I stopped investing time in it, so I am not very informed on what D is capable of.

##### Rust advantages over D

+ At this moment, there is no other native language that can offer the same level of safety that Rust can offer. Even most of the garbage collected languages can’t offer the same level of safety as Rust does(no data races).

+ Rust has a powerful macros system. You can for example, at compile time, download a file from the internet and then take its input to generate some data you will need at run-time - yes, that powerful.
A good example of the power of the Rust macros system would be the regex crate72, where it will check at compile-time if your regex is actually valid(and fail to compile if not) and the regex itself will turn into an optimized regex tailored to your specific need, it would be like a hand written optimized regex.
Another example are database crates, like diesel79 that can make sure at compile-time that you don’t make errors in your queries(not misspellings but actual errors). Or rust-postgres-macros68 that makes sure the SQL query is valid

+ Rust’s type system(combined with the borrow checker) offers a lot of power to library writers.
A library can force its users to use it correctly. Making sure users don’t make mistakes.
Here is an example how even in low-level code Rust type system can help enforce correct usage - note that the article is a bit more complex and understanding Rust semantics might be necessary.

There are probably more points but it’s probably better to keep it shorter.  
I think the first point should be enough to convince anybody.  
I work at a company that uses C++ exclusively for its projects. The projects are very big and it’s interesting that we are always left astonished with what kind of complex bugs cripple in, mostly related to threading but sometimes also related to memory management.  
And I can’t express how hard it is to find bugs in very big projects, it gets so complex.  
We had one bug that we jumped around the code for a long time only to find in the end that that general function that was cleaning every time our vectors, was doing nasty things to a vector that was storing smart pointers, zeroing the memory, thus never getting the reference count to 0 and then free the heap allocated memory.  
Now that I think about it, D actually can’t help with any of our real issues while those bugs would of been avoided with Rust.


##### Rust disadvantages compared to D

+ Because correctness is enforced(code logic can still be totally wrong), the learning curve in Rust is big, especially taking into consideration that D has C-like syntax, it is very familiar to most programmers(not beginners of course).
And that’s basically the main issue with Rust, it’s learning curve. You have to decide if you want to invest time in understanding why the compiler doesn’t allow you to compile that code in order to have all the advantages Rust offers you.

+ D has been in the wild for a longer time. My expectation would be that some libraries are in better state.
I don’t how D is doing at this category, but I think Rust doesn’t yet have a big collection of good libraries.
C++ for example is very rich in this area, take Boost or open github at any big company, like Facebook’s Github for example. Only opening Facebook’s Github you will find a big collection of high-quality C++ libraries.

In the end, for a language to take off(user base wise) it would need a big company backing it up.
Best example of this would be Apple with Objective-C(and now Swift). They didn’t only promote it, they made it the de facto programming language to write software for their system.
To compare this to D and Rust, that would mean that Facebook would have to make D the de facto language to write Facebook plugins and Mozilla to make Rust the de facto language to write extensions for Firefox.
Of course these use cases cannot compete with writing `full-fledged software` for an `operating system` but it would change a lot.