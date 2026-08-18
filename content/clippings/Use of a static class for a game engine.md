---
title: "Use of a static class for a game engine"
source: "https://codereview.stackexchange.com/questions/77513/use-of-a-static-class-for-a-game-engine?rq=1"
author:
  - "[[heyufool1heyufool1                    7311 silver badge44 bronze badges]]"
  - "[[Emily L.Emily L.                    16.7k11 gold badge3939 silver badges8989 bronze badges]]"
  - "[[heyufool1–                         heyufool1]]"
  - "[[nwp–                         nwp]]"
  - "[[Emily L.–                         Emily L.]]"
  - "[[MorwennMorwenn                    20.2k33 gold badges6969 silver badges132132 bronze badges]]"
published: 2015-01-14
created: 2025-09-21
description: "I've been designing a game engine for the past few months with little issues.  However, one main goal with this project is to put it on my portfolio/résumé so naturally I want the code to be as goo..."
tags:
  - "clippings"
---
Asked

Modified [10 years, 8 months ago](https://codereview.stackexchange.com/questions/77513/?lastactivity "2015-01-14 20:18:07Z")

Viewed 5k times

I've been designing a game engine for the past few months with little issues. However, one main goal with this project is to put it on my portfolio/résumé so naturally I want the code to be as good as possible. With that in mind, I got a little worried today because I designed a fair amount of my engine around using static classes. However, I always read that statics are bad, evil, and break OOP among other negative things.

Is my use of the static classes in my game bad design that should be changed (despite working, and personally finding it easy to understand and intuitive) or is it acceptable use? Keep in mind I want employers to look at this project as an example of my programming ability, which is why I'm asking this about my specific situation, in addition to reading all the related posts as possible.

For an example of a static class, I have my `Game` class:

```cpp
#ifndef _GAME_H_
#define _GAME_H_

#include "common.h"

class btDiscreteDynamicsWorld;

class Game 
{
friend class Drawing;

public:
    // Initializes the game by creating the application window, initializing OpenGL, and starting the main game loop.
    static void initialize(std::string gameName, HINSTANCE hInstance);

    // Get the handle to the Windows based application window.
    static HWND getAppWindow(void);

    // Returns the dynamic world (physics world) used by the game.
    static btDiscreteDynamicsWorld* getDynamicsWorld(void) { return sDynamicsWorld; }

    // Returns the time, in seconds, that it took the last frame to fully execute.
    static float getTimeElapsed(void);

    // Sets the game's active status to either true, or false (not active).  The game and its application window will not update.
    static void setActive(bool active);

private:
    // Creates the game's application window.
    static bool createAppWindow(void);

    // Creates a temporary  fake window for the use of GLEW to load OpenGL's functions
    static HWND createFakeWindow(void);

    // The main game loop where all updating and rendering is done.
    static void mainLoop(void);

    // Process Windows' messages to the application window.
    static LRESULT CALLBACK messageHandler(HWND hWnd, UINT uiMsg, WPARAM wParam, LPARAM lParam);

    static LRESULT CALLBACK simpleMessageHandler(HWND hWnd, UINT uiMsg, WPARAM wParam, LPARAM lParam);

    // Resets the main game timer.
    static void resetTimer(void);

    static btDiscreteDynamicsWorld* sDynamicsWorld;
    static bool sIsActive;
    static bool sIsInitialized;
    static std::string sGameName;
    static HINSTANCE sHInstance;
    static HANDLE mHMutex;
    static HWND sHWnd;
    static DWORD sLastTickCount;
    static float sTimeElapsed;
};

#endif
```

The source of this class includes the entry point that calls `initialize()` which starts the whole process of starting up the game, and eventually starts the main loop. The point of the class is that any of my other classes can simply include the header then, for example, use `Game::getTimeElapsed()` to get the time since the last frame. I find this great since any class can have access to game necessary features, in addition there is privatization so I can choose what I want and don't want to be "global". Also, if I were to make it an instanced class, then I would have to pass around an instance of it to anything that needs simple game related features. My reasoning for this being perfectly acceptable and not evil is that I never ever want more than one `Game` at once, and I never want to recreate it.

Now that you have an idea of what my design is (I use the same idea for various other aspects such as `Drawing` and `Input`), do you think this is bad design? And why?

Addressing "loose" code: I've read a lot that people frown on this because it makes the code loose, and they find this the lazy approach to just sending references of a `Game` instance to any object that needs it, claiming that makes it tighter code. However, I don't understand that logic because in order to use the reference you would still need to `#include "game.h"`, so any file using the instanced `Game` would need that include and the reference. The same applies to my static class except you don't need the instance (rather it's not allowed). Files that need access to `Game` still have to include the file, so I guess I just don't understand how including the header and a reference is tighter code than just including the header.

Also, I hear people say generically, particularly one professor of mine, that you don't know who would be changing/accessing a class if it's static, and global with the use of the header. Which I don't understand as well, because I know who can change the `Game` class, which is only files that I explicitly typed in `#include "game.h"` in their source files. I guess mainly I don't understand how someone who is writing all of their own code say, "I don't know who will be changing this object", but you do! Only code that you typed in to reference it, to me it almost seems like they're saying some code magically or unknowingly changes it, which shouldn't be the case since you should know what code you have typed in and where it changes other objects.

I feel like I may be missing the bigger picture, but I've been stubborn on this subject ever since I started programming so any enlightenment would be greatly appreciated.

Addressing "bad OOP design": I am using C++ which is obviously OOP, but why does that mean everything needs to follow perfect object oriented design? Not everything in a program needs to be an object in my mind. For example, the game itself is an object, but there can only ever be one of them (and it will only ever be "created" once), so what could be the advantage of making it a class that can be instanced? With multi-threading aside (I don't know how that applies to static classes, but I think I read that it has issues with it), how could forcing a class to always exist, and to only ever exist once bad design? To me, it's the same as doing `Game* game = new Game()`, and never deleting, or creating another `Game`, however with my design it has the advantage of not giving the user the ability to recreate the game (which is a feature I want).

How can making an "object" be an object that has to exist, that can't be explicitly deleted or replaced be considered bad design? In a literal interpretation of my `Game` class, why would I ever want to create another `Game` when one is already forced to exist? I say specifically talk about create because I feel that's the only advantage of a class that can be instantiated over a static class.

Yes, I do believe that this is a bad practice. And as a presumptive employer I would be worried and put your application towards the bottom of the pile.

What you are doing is essentially a singleton pattern but you're not treating it as such. The singleton pattern is one of the most basic design patterns (and probably most frequently abused). This tells me you have limited knowledge about design patterns and code design.

You are also just taking procedural code and trying to make it look like it is object oriented while it really is not. Which tells me as an employer that "you just don't get object oriented programming".

The exact same API and features could have been implemented with a namespace like this:

```cpp
namespace Game{
    void initialize(std::string gameName, HINSTANCE hInstance);
    ...
}
```

and you would have all the private members from your class as globals in the `cpp` file. This is the exactly the same thing as what you're doing. You're abusing a `class` as a `namespace`. While I do not condone this particular design for the problem at hand, the namespace approach would have placed you a bit higher up in the pile of applicants, because at least you're not abusing object orientation and I can accept the namespace approach as a convenient design decision.

Had you instead properly used the singleton pattern where it is suitable, like this:

```cpp
class Game{
public:
    void createWindow(const std::string& title);
    ....

    static Game& instance(){
        static Game game;
        return game;
    }
private:
    Game();
    Game(const Game&) = delete;
    Game(Game&&) = delete;
    void operator=(const Game&) = delete;
    void operator=(Game&&) = delete;
};

int main(int, char**){
    Game::instance().createWindow("My Game");
}
```

You would have soared to the top of the pile of applicants.

> Addressing "bad OOP design": I am using C++ which is obviously OOP,

Let me stop you right there buddy! Just because you are using a C++ compiler, doesn't mean your code is object oriented. Lots of C, and procedural code compiles perfectly fine under C++. What the language is and how you use it are two entirely different things. Just because you can use a wrench to hammer a nail, doesn't make it a hammer.

> ...but why does that mean everything needs to follow perfect Object Oriented design? Not everything in a program needs to be an object in my mind.

Not *everything* needs to be object oriented. But don't use a `class` if you are not writing object oriented code.

> For example, the game itself is an object, but there can only ever be one of them (And it will only ever be "created" once),

This my friend is what singletons are for.

> so what could be the advantage of making it a class that can be instanced?

The singleton pattern as I implemented it has well defined construction and destruction which means that all code paths that exit the program normally will invoke the destructor and perform clean up. You do not need to call `deinitialize/shutdown` explicitly to clean up.

The standard guarantees that memory for `class/struct` members will be laid out contiguously in memory which is good for your cache hit/miss ratio. Granted that the compiler may likely place your statics contiguously as well, this is not guaranteed though.

If you at some point decide to allow multiple game instances, say you make a multiplayer server, object oriented code is much easier to adapt.

> With multi-threading aside (I don't know how that applies to static classes, but I think I read that it has issues with it), how could forcing a class to always exist, and to only ever exist once bad design?

Again it is not bad design but use the correct pattern for it. And yes, statics tend to complicate things when you start multithreading but in your case it is no less complicated if using the singleton pattern.

> To me, it's the same as doing Game\* game = new Game(), and never deleting, or creating another Game, however with my design it has the advantage of not giving the user the ability to recreate the game (Which is a feature I want).

The singleton pattern has all those properties with the benefit of automatic destruction when your application terminates by normal means.

> So, how can making an "object" be an object that has to exist, that can't be explicitly deleted or replaced bad design.

As I said, it is not bad design per say. Although it makes testing in isolation with unit tests difficult. Masquerading procedural code as a class is a big no-no for me.

> In a literal interpretation of my Game class, why would I ever want to create another Game when one is already forced to exist? I say specifically talk about create because I feel that's the only advantage of a class that can be instantiated over a static class.

12

Don't worry, keep calm, your design is not a bad one. Concerning the "bad OOP design", don't worry either: [C++ is not an object-oriented](https://isocpp.org/blog/2014/12/myths-1) (see bullet 2), it is a multi-paradigm language which happens to provide a way to do object-oriented programming as one of its many tools. Here is why your design is not bad:

- You don't need multiple instances of `Game`.
- You need `private` access to some members.
- Your design is easy to use and hard to get wrong.

Now, here are some things worth discussing:

- While two-steps initializations may sometimes be needed (I don't think it is in your case), constructors and destructors are great tools. Moreover, C++ generally advocates to acquire resources at construction and to release them at destruction (that's [RAII](http://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization)).
- Instead of using a singleton pattern, you could opt for a [Monostate pattern](http://c2.com/cgi/wiki?MonostatePattern) which is kind of a mix between what you did and a singleton: everything is `static` and it has a check in its constructor to initialize it only once. That way you can pass it around or simply call `Game().something()` to call the function.
- However, my favourite pattern for this kind of things would be the [Service Locator](http://gameprogrammingpatterns.com/service-locator.html) pattern. Agreed it's overkill for a game engine, but you could break your game engine into several subengines (audio, random numbers, UI, etc...) and use this pattern for the different services and cross-cutting concerns in your code. Using service locators also allows to use empty implementations when you want to turn off a service during development.
- You could also consider not doing a singleton, a monostate nor a `static` class and then manually ensure that you only create it once. Seriously, it's not that hard in a game. Sometimes, using dependency is not that bad when you know what to pass and when to pass it. For example, instead of passing the `Game` instance around, you could pass its different components (or services).

Anyway, there is a choice to make and it is yours. However, there are some details in your code that do not have anything to do with singletons and stuff and which need to be fixed anyway:

- `_GAME_H_` begins with an uderscore followed by a capital letter. Therefore it is [reserved to the implmentation](https://stackoverflow.com/a/228797/1364752) and using it *should* make your programmed ill-formed (it always compile in practice). You better use `GAME_H_` instead if you want to be pedantic.
- In C++, you don't have to specify `void` when your function does not take any parameter; that works but it's more of a C rule. If you want to be idiomatic, remove the `void` in function parameter lists.
- `createAppWindow` and `createFakeWindow` look dangerously similar but don't return the same type. Without care, I would supposed that they are used the same way. You may want to pick better names.
- Using Doxygen for the documentation could be a good idea (or any equivalent code documentation software).
- You may want to abstract away the system-specific things into some classes (or into a `System` class) so that your code deosn't only depend on the Windows API. Even if you don't intend to do it right now, having an interface to abstract away the system-specific things would allow you to port your code to other systems in the future.

7