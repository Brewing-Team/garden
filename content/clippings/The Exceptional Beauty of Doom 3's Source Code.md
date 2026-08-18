---
title: "The Exceptional Beauty of Doom 3's Source Code"
source: "https://kotaku.com/the-exceptional-beauty-of-doom-3s-source-code-5975610"
author:
  - "[[Shawn McGrath]]"
published: 2016-08-22
created: 2025-09-27
description: "This is a story about Doom 3’s source code and how beautiful it is. Yes, beautiful. Allow me to explain. After releasing my video game Dyad I took a"
tags:
  - "clippings"
---
This is a story about *Doom 3* ’s source code and how beautiful it is. Yes, *beautiful*. Allow me to explain.

After releasing my video game [*Dyad*](http://www.dyadgame.com/) I took a little break. I read some books and watched some movies I’d put off for too long. I was working on the European version of *Dyad*, but that time was mostly waiting for feedback from Sony quality assurance, so I had a lot of free time. After loafing around for a month or so I started to seriously consider what I was going to do next. I wanted to extract the reusable/engine-y parts of *Dyad* for a new project.

<video aria-label="Connatix video player" role="application" title="" src="blob:https://kotaku.com/ff2b49c0-0bd8-4f34-8fcf-9c0831671f57"></video>

<audio></audio>

<audio></audio>

1/1

**This article originally appeared January 14, 2013.**

When I originally started working on *Dyad* there was a very clean, pretty functional game engine I created from an accumulation of years of working on other projects. By the end of *Dyad* I had a hideous mess.

In the final six weeks of *Dyad* development I added over 13k lines of code. MainMenu.cc ballooned to 24,501 lines. The once-beautiful source code was a mess riddled with #ifdefs, gratuitous function pointers, ugly inline SIMD and asm code—I learned a new term: “code entropy.” I searched the internet for other projects that I could use to learn how to organize hundreds of thousands of lines of code. After looking through several large game engines I was pretty discouraged; the *Dyad* source code wasn’t actually that bad compared to everything else out there!

Unsatisfied, I continued looking, and found [a very nice analysis of id Software’s *Doom 3* source code](http://fabiensanglard.net/doom3/index.php) by the computer expert Fabien Sanglard.

I spent a few days going through the *Doom 3* source code and reading Fabien’s excellent article when I tweeted:

It was the truth. I’ve never really cared about source code before. I don’t really consider myself a “programmer.” I’m good at it, but for me it’s just a means to an end. Going through the *Doom 3* source code made me really appreciate good programmers.

---

To put things into perspective: *Dyad* has 193k lines of code, all C++. *Doom 3* has 601k, *Quake III* has 229k and *Quake II* has 136k. That puts *Dyad* somewhere in between *Quake II* and *Quake III*. These are large projects.

When I was asked to write this article, I used it as an excuse to read more source code from other games, and to read about programming standards. After days of research I was confused by my own tweet that started this whole thing: what would “nice looking”—or “beautiful”, for that matter—actually mean when referring to source code? I asked some programmer friends what they thought that meant. Their answers were obvious, but still worth stating:

Code should be locally coherent and single-functioned: One function should do exactly one thing. It should be clear about what it’s doing.

Local code should explain, or at least hint at the overall system design.

Code should be self-documenting. Comments should be avoided whenever possible. Comments duplicate work when both writing and reading code. If you need to comment something to make it understandable it should probably be rewritten.

There’s an idTech 4 coding standard ([.doc](https://ftp.idsoftware.com/idstuff/doom3/source/CodeStyleConventions.doc)) that I think is worth reading. I follow most of these standards and I’ll try to explain why they’re good and why specifically they make the *Doom 3* code so beautiful.

### Unified Parsing and Lexical Analysis

One of the smartest things I’ve seen from *Doom* is the generic use of their lexical analyzer\[[1](https://kotaku.com/#ftn.id001)\] and parser \[[2](https://kotaku.com/#ftn.id002)\]. All resource files are ascii files with a unified syntax including: scripts, animation files, config files, etc; everything is the same. This allows all files to be read and processed by a single chunk of code. The parser is particularly robust, supporting a major subset of C++. By sticking to a unified parser and lexer all other components of the engine needn’t worry about serializing data as there’s already code for that. This makes all other aspect of the code cleaner.

### Const and Rigid Parameters

*Doom* ’s code is fairly rigid, although not rigid enough in my opinion with respect to const\[[3](https://kotaku.com/#ftn.id003)\]. Const serves several purposes which I believe too many programmers ignore. My rule is “everything should always be const unless it can’t be”. I wish all variables in C++ were const by default. *Doom* almost always sticks to a “no in-out” parameter policy; meaning all parameters to a function are either input or output never both. This makes it much easier to understand what’s happening with a variable when you pass it to a function. For example:

This function definition this makes me happy!

Just from a few consts I know many things:

The idPlane that gets passed as an argument will not be modified by this function. I can safely use the plane after this function executes without checking for modifications of the idPlane.

I know the epsilon won’t be changed within the function, (although it could easily be copied to another value and scaled for instance, but that would be counter productive)

front, back, frontOnPlaneEdges and backOnPlaceEdges are OUT variables. These will be written to.

the final const after the parameter list is my favourite. It indicates idSurface::Split() won’t modify the surface itself. This is one of my favourite C++ features missing from other languages. It allows me to do something like this:void f(const idSurface &s) {  
s.Split(….);  
}if Split wasn’t defined as Split(…) const; this code would not compile. Now I know that whatever is called f() won’t modify the surface, even if f() passes the surface to another function or calls some Surface::method(). Const tells me a lot about the function and also hints to a larger system design. Simply by reading this function declaration I know surfaces can be split by a plane dynamically. Instead of modifying the surface, it returns new surfaces, front and back, and optionally frontOnPlaneEdges and backOnPlaneEdges.

The const rule, and no input/output parameters is probably the single most important thing, in my eyes, that separate good code from beautiful code. It makes the whole system easier to understand and easier to edit or refactor.

### Minimal Comments

This is a stylistic issue, but one beautiful thing that *Doom* usually does is not over-comment. I’ve seen way too much code that looks like:

I find this extremely irritating. I can tell what this method does by its name. If its function can’t be inferred from its name, its name should be changed. If it does too much to describe it in its name, make it do less. If it really can’t be refactored and renamed to describe its single purpose then it’s okay to comment. I think programmers are taught in school that comments are good; they aren’t. Comments are bad unless they’re totally necessary and they’re rarely necessary. *Doom* does a reasonable job at keeping comments to a minimum. Using the idSurface::Split() example, lets look at how it’s commented:

// splits the surface into a front and back surface, the surface itself stays unchanged  
// frontOnPlaneEdges and backOnPlaneEdges optionally store the indexes to the edges that lay on the split plane  
// returns a SIDE\_?

The first line is completely unnecessary. We learned all that information from the the function definition. The second and third lines are valuable. We could infer the second line’s properties, but the comment removes potential ambiguity.

*Doom* ’s code is, for the most part, judicial with its comments, which it makes it much easier to read. I know this may be a style issue for some people, but I definitely think there is a clear “right” way to do it. For example, what would happen if someone changed the function and removed the const at the end? Then the surface \*COULD\* be changed from within the function and now the comment is out of sync with the code. Extraneous comments hurt the readability and accuracy of code thus making the code uglier.

### Spacing

*Doom* does not waste vertical space:

Here’s an example from t\_stencilShadow::R\_ChopWinding():

I can read that entire algorithm on 1/4 of my screen, leaving the other 3/4s to understand where that block of code fits relative to its surrounding code. I’ve seen too much code like this:

This is going to be another point that falls under “style.” I programmed for more than 10 years with the latter style, forcing myself to convert to the tighter way while working on a project about six years ago. I’m glad I switched.

The latter takes 18 lines compared to 11 in the first. That’s nearly double the number of lines of code for the \*EXACT\* same functionality. It means that the next chunk of code doesn’t fit on the screen for me. What’s the next chunk?

That code makes no sense without the previous for loop chunk. If id didn’t respect vertical space, their code would be much harder to read, harder to write, harder to maintain and be less beautiful.

Another thing that id does that I believe is “right” and not a style issue is they \*ALWAYS\* use { } even when optional. I think it’s a crime to skip the brace brackets. I’ve seen so much code like:

That is ugly code, it’s worse than than putting { } on their own line. I couldn’t find a single example in id’s code where they skipped the { }. Omitting the optional { } makes parsing this while() block more time consuming than it needs to be. It also makes editing it a pain, what if I wanted to insert an if-statement branch within the else if (c > d) path?

### Minimal Templates

id did a huge no-no in the C++ world. They re-wrote all required STL\[[4](https://kotaku.com/#ftn.id004)\] functions. I personally have a love-hate relationship with the STL. In *Dyad* I used it in debug builds to manage dynamic resources. In release I baked all the resources so they could be loaded as quickly as possible and don’t use any STL functionality. The STL is nice because it provides fast generic data structures; it’s bad because using it can often be ugly and error prone. For example, let’s look at the std::vector class. Let’s say I want to iterate over each element:

That does get simplified with C++11:

I personally don’t like the use of auto, I think it makes the code easier to write but harder to read. I might come around to the usage of auto in the coming years, but for now I think it’s bad. I’m not even going to mention the ridiculousness of some STL algorithms like std:for\_each or std::remove\_if.

Removing a value from an std::vector is dumb too:

Gee, that’s going to be typed correctly by every programmer every time!

id removes all ambiguity: they rolled their own generic containers, string class, etc. They wrote them much less generic than the STL classes, presumably to make them easier to understand. They’re minimally templated and use id-specific memory allocators. STL code is so littered with template nonsense that it’s impossible to read.

C++ code can quickly get unruly and ugly without diligence on the part of the programmers. To see how bad things can get, check out the STL source code. Microsoft’s and GCC’s\[[5](https://kotaku.com/#ftn.id005)\] STL implementations are probably the ugliest source code I’ve ever seen. Even when programmers take extreme care to make their template code as readable as possible it’s still a complete mess. Take a look at [Andrei Alexandrescu’s Loki library](http://loki-lib.sourceforge.net/index.php?n=Main.Download), or the [boost libraries](http://www.boost.org/) —these are written by some of the best C++ programmers in the world and great care was taken to make them as beautiful as possible, and they’re still ugly and basically unreadable.

id solves this problem by simply not making things overly generic. They have a HashTable and a HashIndex class. HashTable forces key type to be const char \*, and HashIndex is an int->int pair. This is considered poor C++ practice. They “should” have had a single HashTable class, and written partial specialization for KeyType = const char \*, and fully specialized . What id does is completely correct and makes their code much more beautiful.

This can be further examined by contrasting ‘good C++ practice’ for Hash generation and how id does it.

It would be considered by many to be good practice to create a specific computation class as a parameter to the HashTable like so:

this could then be specialized for a particular type:

Then you could pass the ComputeHashForType as a HashComputer for the HashTable:

This is similar to how I did it. It seems smart, but boy is it ugly! What if there were more optional template parameters? Maybe a memory allocator? Maybe a debug tracer? You’d have a definition like:

Function definitions would be brutal!

What does that even mean? I can’t even find the method name without some aggressive syntax highlighting. It’s conceivable that there’d be more definition code than body code. This is clearly not easy to read and thus not beautiful.

I’ve seen other engines manage this mess by offloading the template argument specification to a myriad of typedefs. This is even worse! It might make local code easier to understand, but it creates another layer of disconnect between local code and the overarching system logic, making the local code not hint towards system design, which is not beautiful. For example, lets say there was code:

and

and you used both and did something like:

It’s possible that the StringHashTable’s memory allocator, StringAllocator, won’t contribute to the global memory, which would cause you confusion. You’d have to backtrack through the code, find out that StringHashTable is actually a typedef of a mess of templates, parse through the template code, find out that it’s using a different allocator, find that allocator… blah blah, ugly.

*Doom* does the complete “wrong” thing according to common C++ logic: it writes things as non-generic as possible, using generics only when it makes sense. What does *Doom* ’s HashTable do when it needs to generate a hash of something? It calls idStr::GetHash(), because the only type of key it accepts is a const char \*. What would happen if it needs a different key? My guess is they’d template the key, and force just call key.getHash(), and have the compiler enforce that all key types have an int getHash() method.

### Remnants of C

I don’t know how much of id’s original programming team is with the company anymore, but John Carmack at least comes from a C background. All id games before *Quake III* were written in C. I find many C++ programmers without a strong C background over-C++ize their code. The previous template example was just one case. Three other examples that I find often are:

over-use set/get methods

use stringstreams

excessive operator overloading.

id is very judicial in all these cases.

Often one may create a class:

This is a waste of lines of code and reading time. It takes longer to write it, and read it compared to:

What if you’re often increasing var by some number n?

vs

The first example is much easier to read and write.

id doesn’t use stringstreams. A stringstream contains probably the most extreme bastardization of operator overloads I’ve ever seen: <<. For example: That’s ugly. It does have strong advantages: you can define the equivalent of Java’s toString() method per class w/o touching a class’ vtables, but the syntax is offensive, and id chose to not use. Choosing to use printf() instead of stringstreams makes their code easier to read, and thus I think it’s the correct decision. Much nicer! The syntax for SomeClass’ operator << would be ridiculous too: \[**Side note:** John Carmack has stated that static analysis tools revealed that their common bug was incorrect parameter matching in printf(). I wonder if they’ve changed to stringstreams in *Rage* because of this. GCC and clang both find printf() parameter matching errors with -Wall, so you don’t need expensive static analysis tools to find these errors.\]

Another thing that makes the *Doom* code beautiful is the minimal use of operator overloads. Operator overloading is a very nice feature of C++. It allows you to do things like:

Without overloading these operations would be more time consuming to write and parse. *Doom* stops here. I’ve seen code that doesn’t. I’ve seen code that will overload operator ‘%’ to mean dot product or operator Vector \* Vector to do piece-wise vector multiplication. It doesn’t make sense to make the \* operator for cross product because that only exists in 3D, what if you wanted to do:  
some\_2d\_vec \* some\_2d\_vec, what should it do? What about 4d or higher? id’s minimal operator overloading leaves no ambiguity to the reader of the code.

### Horizontal Spacing

One of the biggest things I learned from the *Doom* code was a simple style change. I used to have classes that looked like:

According to id’s *Doom 3* coding standard, they use real tabs that are 4 spaces. Having a consistent tab setting for all programmers allows them horizontally align their class definitions:

They rarely put the inline functions inside the class definition. The only time I’ve seen it is when the code is written on the same line as the function declaration. It seems this practice is not the norm and is probably frowned upon. This method of organizing class definitions makes it extremely easy to parse. It might take a little more time to write, since you’d have re-type a bunch of information when defining the methods:

I’m against all extra typing. I need to get stuff done as fast as possible, but this is one situation where I think a little extra typing when defining the class more than pays for itself each time the class definition needs to be parsed by a programmer. There are several other stylistic examples provided in the *Doom 3* Coding Standards ([.doc](https://kotaku.com/%20ftp://ftp.idsoftware.com/idstuff/doom3/source/CodeStyleConventions.doc)) that contribute to the beauty of *Doom* ’s source code.

### Method Names

I think *Doom* ’s method naming rules are lacking. I personally enforce the rule that all method names should begin with a verb unless they can’t.

For example:

is much better than:

### Yes, it’s Beautiful.

I was really excited to write this article, because it gave me an excuse to really think about what beautiful code is. I still don’t think I know, and maybe it’s entirely subjective. I do think the two biggest things, for me at least, are stylistic indenting and maximum const-ness.

A lot of the stylistic choices are definitely my personal preferences, and I’m sure other programmers will have different opinions. I think the choice of what style to use is up to whoever has to read and write the code, but I certainly think it’s something worth thinking about.

I would suggest everyone look at the *Doom 3* source code because I think it exemplifies beautiful code, as a complete package: from system design down to how to tab space the characters.

*Shawn McGrath is a Toronto-based game developer and the creator of the acclaimed PlayStation 3 psychedelic puzzle-racing game Dyad. Find out more about* [*his game*](http://www.dyadgame.com/)*. Follow him* [*on Twitter*](https://twitter.com/DyadGame)

---

**Footnotes**

\[[1](https://kotaku.com/#id001)\] A lexical analyzer converts the characters of source code, (in the relevent context), into a series of tokens with semantic significance. Source code may look like:

x = y + 5;

A lexical analyzer (or “lexer” for short), might tokenize that source as such:  
x => variable  
\= => assignment operator  
y => variable  
\+ => additional operator  
5 => literal integer  
; => end statement

This string of tokens is the first of many steps in converting source code to a running program. following lexical analysis the tokens are fed into a parser, then a compiler, then a linker, and finally a virtual machine, (in the case of compiled languages a CPU). There can be intermediate steps inserted between those main steps, but the ones listed are generally considered to be the most fundamental.

\[[2](https://kotaku.com/#id002)\] A parser is (usually) the next logical step following lexical analysis in machine understanding of language, (computer language/source code in this context, but the same would apply for natural language). A parser’s input is a list of tokens generated by a lexical analyzer, and outputs a syntactic tree: a “parse tree.”

In the example: x = y + 5, the parse tree would look like:

\[[3](https://kotaku.com/#id003)\] “const” is a C++ keyword that ensures that a variable cannot be changed, or that a method will not change the contents of its class. “const” is shortform for “constant.” It’s worth noting that C++ includes a workaround, either via const\_cast\[T\] or a C-style cast: (T \*). Using these completely breaks const, and for the sake of argument I prefer to ignore their existence and never use them in practice.

\[[4](https://kotaku.com/#id004)\]STL stands for “standard template library” It’s a set of containers, algorithms, and functions commonly used by C++ programmers. It’s supported by every major compiler vendor with varying levels of optimization and error reporting facilities.

\[[5](https://kotaku.com/#id005)\]GCC – GNU Compiler Collection: a set of compiler supporting multiple programming languages. For the case of this article it refers to the GNU C/C++ compiler. GCC is a free compiler, with full source code available for free and works on a wide array of computers and operating systems. Other commonly used compilers include: clang, Microsoft Visual C++, IBM XL C/C++, Intel C++ Compiler.