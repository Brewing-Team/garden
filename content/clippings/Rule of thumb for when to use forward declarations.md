---
title: "Rule of thumb for when to use forward declarations?"
source: "https://www.reddit.com/r/cpp/comments/1gyeyj3/rule_of_thumb_for_when_to_use_forward_declarations/"
author:
  - "[[[deleted]]]"
published: 2024-11-24
created: 2025-09-21
description:
tags:
  - "clippings"
---
This was my rule so far: **If i dont need definitions in the header, i forward declare a class and include the definition in the .cpp if needed.**

**What do you guys think about this?**

---

## Comments

> **mbechara** • [13 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lypo0b8/) •
> 
> From a design perspective, using forward declarations can reduce coupling between classes, i.e., if class A depends on class B, but class A doesn't need to know the size of B, then class A doesn't need the full declaration of class B exposed to it. In this case you use forward declaration and thus reduce class coupling.
> 
> Also manually writing the forward declaration inline where it's needed can be problematic or downright cumbersome to read, and thus it's recommended to use a .fwd.hpp file instead. For example, if today you have:
> 
> #ifndef FOO\_HPP
> #define FOO\_HPP
> 
> class Bar;
> 
> void foo(Bar\* bar);
> 
> #endif
> 
> Here one can argue that there is little value for a .fwd file. But let's say someday you need to place Bar into a namespace, or maybe change its namespace for any reason:
> 
> #ifndef FOO\_HPP
> #define FOO\_HPP
> 
> namespace baz::bar
> {
> class Bar;
> }
> 
> void foo(Bar\* bar);
> 
> #endif
> 
> This is problematic as now you need to find and update each file where you manually have the forward declaration inline, but moreover, with multiple forward declarations, it quickly becomes less cleaner/readable.  
> So better use a .fwd.hpp file for each .hpp file that **you need to have** a forward declaration for, or you can always use a global .fwd.hpp file for your library.
> 
> I'd like to add that a .fwd.hpp can hold entities that are shared between multiple files there, but are conceptually related to the .hpp file of that .fwd.hpp.
> 
> track me
> 
> > **\[deleted\]** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyqizak/) •
> > 
> > Awesome response, thanks!

> **QuentinUK** • [7 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyo4a9q/) •
> 
> This is what I do as much as possible as it saves time compiling.
> 
> class MyClass;
> 
> std::vector<MyClass> my\_school;
> 
> Google discourages forward declarations if you’re interested in further details you can read about it here:- [https://google.github.io/styleguide/cppguide.html#Forward\_Declarations](https://google.github.io/styleguide/cppguide.html#Forward_Declarations)
> 
> > **TomDuhamel** • [16 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyo8mid/) •
> > 
> > > Google discourages forward declarations
> > 
> > I just read that, and while their arguments are correct and valid, I disagree with their conclusion and recommendation. I absolutely avoid including project headers in each other and use forward declarations whenever possible.
> > 
> > > **lord\_braleigh** • [23 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyoio52/) •
> > > 
> > > It’s advice for Googlers, not for the rest of us. Google has thousands of engineers making changes and a program which automatically handles header inclusion. So their advice is tailored to letting the automation work and making your code robust to frequent changes.
> 
> **timbeaudet** • [3 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyo69fc/) •
> 
> Just in case, for some containers the standard does not specify they must work with forward declared types; ie full type must be known. The vector you mention here isn’t on of those but I somewhat recently ran into this with a std::unordered\_map I think it was and learned.
> 
> > **die\_liebe** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyrdjp4/) •
> > 
> > Yes, std::map works with incomplete type, while std::unordered\_map doesn't.
> > 
> > (But I think that the standard does not guarantee it for std::map, so I don't recommend relying on it.)
> > 
> > > **timbeaudet** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyrisrt/) •
> > > 
> > > std::unordered\_map can also work (in some cases) with forward declared types. I was just pointing out the gap that some containers don't.
> 
> **\[deleted\]** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyobjf0/) •
> 
> But it really only saves time compiling and doesnt have an effect on the runtime, right?
> 
> > **BenedictTheWarlock** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyp8mzf/) •
> > 
> > If you forward declare a type and store it as a pointer, rather than as a simple value then you may pay a runtime cost for the indirection.
> > 
> > **n1ghtyunso** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lypjabz/) •
> > 
> > it also solves circular header dependencies if you have those somewhere. but ideally you don't have those in the first place.
> > 
> > they are also used in template metaprogramming, but here it's usually forward declaration directly followed by a template specialization of it.
> > 
> > but yea, generally Forward declarations only avoid parsing code that is not needed at their location

> **VinnieFalco** • [3 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyr2122/) •
> 
> I like minimizing the amount of header material so yes

> **Ill-Telephone-7926** • [10 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyosbfh/) •
> 
> A source of busywork. Perhaps best avoided except if optimizing a slow build.
> 
> - Selecting the correct forward declarations is more work than #including the canonical definition.
> - Maintaining the correct forward declaration is brittle.
> - Incomplete declarations can change the meaning of code.
> - Modern code uses value types and smart pointers, so often requiring type definitions.
> 
> > **bert8128** • [9 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lypj11m/) •
> > 
> > If you have thousands of headers and millions of lines of codes then by always including the headers you increase the amount of compilation work significantly for both incremental and full builds.
> > 
> > Here’s an extreme example. You have a class A with a private method that returns a class B by value. That type is not mentioned anywhere else in the header. If you include B.h in A.h you have now made all consumers of A dependent on B.h, which is entirely unnecessary. If B.h changes you now have to compile more files, and they will take longer to compile because of the code in B.h.
> > 
> > Smart pointers do not require that the type is known. Say A.h refers to unique\_ptr<B>. You can avoid a consumer being dependent on B.h by defining A’s destructor in the cpp, rather than the header.
> > 
> > And don’t forget that importing headers imports defines. Not nice.
> > 
> > Can you give examples of your 2nd and 3rd points? Ie how forward declarations lead to brittle code, and can change the meaning?
> > 
> > **donalmacc** • [4 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyrwroj/) •
> > 
> > I disagree that it’s a source of busywork - it’s an incredibly easy optimisation to build times that can have enormous impacts. At a previous job, I spent about 2 weeks picking apart unnecessary includes and replacing them with forward dependencies. I reduced our clean builds by 10 minutes, and reduced incremental builds for the most common files that the team I was on from 30s to 3s.
> > 
> > I could have spent two weeks on somethjng else if the team had paid more attention to it in the first place.
> > 
> > **Nicksaurus** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyq2kql/) •
> > 
> > It's just sad that we waste so much time thinking about this in the first place. I wish we had a better compilation model
> > 
> > > **bert8128** • [3 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lys67zd/) •
> > > 
> > > Modules (when they finally work) will remove this debate.
> > > 
> > > > **Nicksaurus** • [0 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lysl8cb/) •
> > > > 
> > > > Maybe C++20 will finally be complete by the year 2030

> **bert8128** • [0 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyo3oq2/) •
> 
> If you can use a forward declaration why wouldn’t you?
> 
> Ok, there are times when you want to put the implementation of a function in the header so it can be inlined. But mostly just forward declare (and don’t forget you can forward declare return types by value).
> 
> > **\[deleted\]** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyobmzx/) •
> > 
> > Thanks, appreciate your answer :)
> > 
> > **bert8128** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lys6y25/) •
> > 
> > Rather than downvotes how about a useful response?

> **VoodaGod** • [\-1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lypbk71/) •
> 
> unless there is some static analysis tool that enforces this or there is no other way, i refuse to use forward declares. i find them silly as a concept, just include the header, it's what it's for. also include what you use sometimes gets confused and marks a header included in the cpp file as not directly used even though it is needed because the type was only forward declared in the header

> **MellowTones** • [0 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lypjyol/) •
> 
> If a library has enough header content to make it undesirable to include constantly, it should provide a forward declaration header, which is then included by the normal header to ensure consistency, and any cpp/cc file indirectly. The Standard Library <iosfwd> header is an example of this best-practice.
> 
> Don’t make your own forward declarations - things can change in the header - e.g. a struct can become a template with a default argument, which should not stop client code from recompiling but will break yours.

> **sjepsa** • [0 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyr9e3s/) •
> 
> Best practice for compile speed.
> 
> However, worse for portability, code modification and possible bugs
> 
> > **bert8128** • [2 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lys75ry/) •
> > 
> > Can you give some examples samples of the problems?
> > 
> > > **sjepsa** • [0 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lys7ws5/) •
> > > 
> > > If I remember correctly, it can happen that forward declaration is different by a type to the actual implementation and all kinds of shit happen
> > > 
> > > But I may be a bit rusty, moved to header only 12 years ago
> > > 
> > > > **Livid-Serve6034** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lysf7el/) •
> > > > 
> > > > How did that work out for you? I developed a fairly large project header-only 10 years ago, but because it used templates extensively, adding more code to it increased compilation time exponentially. At one time g++ needed 12G memory to compile the application and it took 30 minutes (for single main.cpp).

> **bakedbread54** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lyqff69/) •
> 
> I only use them as you stated to break circular dependencies. Otherwise, for example if I rename a class, I will have to change all the forward declarations, which would be a massive PITA.

> **Low-Ad4420** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lz7rkuh/) •
> 
> I use forward declarations in the same situation as you. At work we develop software modularly, with small, self-contained libraries and it's important to hide the details on the headers as much as possible. We started doing this because of windows redeclaration problems, conflicting defines and that sort of stuff. If it's hidden within the cpp you won't have any problems including the header on another unit.

> **jhasse** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lz9safx/) •
> 
> I also use this rule, no problems so far.

> **Meleneth** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lzhibrt/) •
> 
> for myself on my projects, I put all my forward declarations and typedefs in one file. That way, all of my headers and implementation files can include just that file and get everything.
> 
> That file becomes the single source of truth, so I never have issues with needing to update the forward declarations in multiple places.
> 
> It massively speeds up compilation times, and makes it really clear when the actual header is really needed. The compiler will point out when you need to include the relevant header in the implementation file.
> 
> [https://github.com/meleneth/rackam/blob/master/src/rackam/rackam\_types.hpp](https://github.com/meleneth/rackam/blob/master/src/rackam/rackam_types.hpp)

> **zl0bster** • [1 points](https://reddit.com/r/cpp/comments/1gyeyj3/comment/lzkgmnt/) •
> 
> [Insane part](https://stackoverflow.com/a/71687477/700825) of C++ related to this:
> 
> It is UB NDR to have `std::unique_ptr` of incomplete type.
> 
> But it compiles. And works for all usecases I ever had.