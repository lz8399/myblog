+++
title= "[Dlang]C++相对D的优点"
date= "2018-06-23T17:58:02+08:00"
categories= ["Dlang"]
tags= ["Dlang", "C++"]
+++

原文：What does C++ do better than D?  
https://softwareengineering.stackexchange.com/questions/97207/what-does-c-do-better-than-d

Most of the things C++ "does" better than D are meta things:   
C++ has better compilers, better tools, more mature libraries, more bindings, more experts, more tutorials etc. Basically it has more and better of all the external things that you would expect from a more mature language. This is inarguable.

As for the language itself, there are a few things that C++ does better than D in my opinion. There's probably more, but here's a few that I can list off the top of my head:

##### C++ has a better thought out type system
There are quite a few problems with the type system in D at the moment, which appear to be oversights in the design. For example, it is currently impossible to copy a const struct to a non-const struct if the struct contains class object references or pointers due to the transitivity of const and the way postblit constructors work on value types. Andrei says he knows how to solve this, but didn't give any details. The problem is certainly fixable (introducing C++-style copy constructors would be one fix), but it is a major problem in language at present.

Another problem that has bugged me is the lack of logical const (i.e. no mutable like in C++). This is great for writing thread-safe code, but makes it difficult (impossible?) to do lazy intialisation within const objects (think of a const 'get' function which constructs and caches the returned value on first call).

Finally, given these existing problems, I'm worried about how the rest of the type system (pure, shared, etc.) will interact with everything else in the language once they are put to use. The standard library (Phobos) currently makes very little use of D's advanced type system, so I think it is reasonable the question whether it will hold up under stress. I am skeptical, but optimistic.

Note that C++ has some type system warts (e.g. non-transitive const, requiring iterator as well as  const_iterator) that make it quite ugly, but while C++'s type system is a little wrong at parts, it doesn't stop you from getting work done like D's sometimes does.

Edit: To clarify, I believe that C++ has a better thought out type system -- not necessarily a better one -- if that makes sense. Essentially, in D I feel that there is a risk involved in using all aspects of its type system that isn't present in C++.

##### D is sometimes a little too convenient
One criticism that you often hear of C++ is that it hides some low-level issues from you e.g. simple assignments like a = b; could be doing many things like calling conversion operators, calling overload assignment operators etc., which can be difficult to see from the code. Some people like this, some people don't. Either way, in D it is worse (better?) due to things like opDispatch, @property, opApply, lazy which have the potential to change innocent looking code into things that you don't expect.

I don't think this is a big issue personally, but some might find this off-putting.

##### D requires garbage-collection
This could be seen as controversial because it is possible to run D without the GC. However, just because it is possible doesn't mean it is practical. Without a GC, you lose a lot of D's features, and using the standard library would be like walking in a minefield (who knows which functions allocate memory?). Personally, I think it is totally impractical to use D without a GC, and if you aren't a fan of GCs (like I am) then this can be quite off-putting.

##### Naive array definitions in D allocate memory
This is a pet peeve of mine:

    int[3] a = [1, 2, 3]; // in D, this allocates then copies
    int a[3] = {1, 2, 3}; // in C++, this doesn't allocate
Apparently, to avoid the allocation in D, you must do:

    static const int[3] staticA = [1, 2, 3]; // in data segment
    int[3] a = staticA; // non-allocating copy
These little 'behind your back' allocations are good examples of my previous two points.

~~Edit: Note that this is a known issue that is being worked on.~~  
Edit: This is now fixed. No allocation takes place.

##### Conclusion
I've focussed on the negatives of D vs C++ because that's what the question asked, but please don't see this post as a statement that C++ is better than D. I could easily make a larger post of places where D is better than C++. It's up to you to make the decision of which one to use.

***
`对的那条路，往往不是最好走的。`