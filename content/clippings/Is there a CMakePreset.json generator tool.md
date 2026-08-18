---
title: "Is there a CMakePreset.json generator tool?"
source: "https://www.reddit.com/r/cmake/comments/17wr3jp/is_there_a_cmakepresetjson_generator_tool/"
author:
  - "[[tjientavara]]"
published: 2023-11-16
created: 2025-10-31
description:
tags:
  - "clippings"
---
I have a small project that uses CMakePresets.json but I am experiencing a combinatorial explosion with the buildPresets. My incomplete buildPresets already causes CMakePresets.json to be over 500 lines in length.

Is there a template language to describe how to generate a CMakePresets.json file, so that we don't have to maintain a large file by hand with the very high chance of making copy-paste mistakes?

See: [https://github.com/hikogui/hikogui/blob/main/CMakePresets.json](https://github.com/hikogui/hikogui/blob/main/CMakePresets.json)

---

## Comments

> **ImRises** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/k9is9sd/) •
> 
> AFAIK there is not real generator, but if i'm not wrong they were a visual interface in visual studio when loading the project and double clicking the json file. I need to check.

> **kisielk** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/k9j156z/) •
> 
> This is pretty normal for CMakePresets.json. My suggestion is to only make presets that you actually need for the project. Typically those are the ones that will actually be used if someone else checks out the repo and needs to build the project, or for CI / testing, etc. If you need a customized preset for a particular development task, add it to CMakeUserPresets.json, which you don't commit to the repo.
> 
> If you want to generate the presets file from code or templates, it's just JSON, so you can use your favorite scripting language to do it.
> 
> > **tjientavara** • [2 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/k9j1o0w/) •
> > 
> > I tent to use most of those.
> > 
> > I need to test with different compilers, with different release modes, and have different build target (since it takes very long to compile everything).
> > 
> > I am not even adding the CI stuff anymore, instead I use CMake command line arguments for that, because this is insane.
> > 
> > > **kisielk** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/k9j2z0b/) •
> > > 
> > > I suggest just writing a Python (or whatever language) script to generate the presets file in that case. Seems like it would be a map of platform -> compiler -> variant and then a combinatorial generation of build presets for each of those.
> > > 
> > > I would also suggest not putting CMAKE\_BUILD\_TYPE in the configure presets and just set the build type in the build preset. That will reduce the number of configure presets. Use multi-config generators like Ninja, VS and Xcode.

> **starball-tgz** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/kd0mr6v/) •
> 
> ... why... are you using `CMAKE_BUILD_TYPE` in an MSVC preset? =.=
> 
> why aren't you using the generator property for your MSVC configure presets?
> 
> > **tjientavara** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/kd11ld9/) •
> > 
> > Because it is not documented by CMake? I don't know what you talking about, just tried to google it. There is no such thing as a "cmake generator property".
> > 
> > > **starball-tgz** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/kd4ae8v/) •
> > > 
> > > @"property", or in proper JSON terminology, "member". [https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html#configure-preset](https://cmake.org/cmake/help/latest/manual/cmake-presets.7.html#configure-preset)

> **keszegrobert** • [1 points](https://reddit.com/r/cmake/comments/17wr3jp/comment/kdj1864/) •
> 
> Yes, there is. It is called CMakeToolchain in conan. [https://docs.conan.io/2.0/reference/tools/cmake/cmaketoolchain.html](https://docs.conan.io/2.0/reference/tools/cmake/cmaketoolchain.html)