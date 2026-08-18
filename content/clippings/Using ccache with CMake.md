---
title: "Using ccache with CMake"
source: "https://crascit.com/2016/04/09/using-ccache-with-cmake/#h-improved-functionality-from-cmake-3-4"
author:
  - "[[Craig Scott]]"
published: 2016-04-09
created: 2025-07-22
description: "Use CMake's launchers to support ccache with GCC, Clang or Xcode, without requiring system-wide installation or symlinks."
tags:
  - "clippings"
---
## Professional CMake:

## A Practical Guide

Learn to use CMake effectively with practical advice from a CMake co-maintainer. You can also have the author work directly with your team!

[GET THE BOOK](https://crascit.com/professional-cmake/) [AUTHOR SERVICES](https://crascit.com/services/)

**Updated 1st February 2017**

Working with very large C/C++ code bases will sometimes test your patience. Build times in particular can be a sore point, especially if the development team do not have a great understanding of how to minimise dependencies between source files, headers, etc. The problem gets worse if the developer frequently switches between branches of their source control system, resulting in source files often changing their contents and/or timestamps. The [ccache](https://ccache.samba.org/) tool aims to minimise that pain by caching compilation outputs (i.e. object files) and reusing them instead of compiling the source again if it gets a compilation request it has seen before and cached. It supports GCC or any compiler that looks like GCC (eg clang). When rebuilding a large project that ccache has mostly compiled before already, the time saving can be significant, even sometimes reducing many minutes down to seconds.

Getting ccache to work with CMake is not overly complicated, but the way to do it is not always obvious. This is especially true with Xcode builds. This article demonstrates how to set up a CMake project to use `ccache` with *Unix Makefiles*, *Ninja* or *Xcode* generators, with Xcode receiving special attention. The techniques presented do not require any changes to the host system. Specifically, no symlinks need to be set up for ccache, making it suitable for use in CI systems, etc. where the developer may not be in control of how/where ccache is installed.  

## Unix Makefiles and Ninja

**Update:** Don’t use `RULE_LAUNCH_COMPILE`  as discussed in this section, use the `CMAKE_<LANG>_COMPILER_LAUNCHER`   approach discussed further below in [Improved functionality from CMake 3.4](https://crascit.com/2016/04/09/using-ccache-with-cmake/#h-improved-functionality-from-cmake-3-4) instead. The other aspects discussed here in this section are still relevant though.

A less well known feature of CMake is the global property called [`RULE_LAUNCH_COMPILE`](https://cmake.org/cmake/help/latest/prop_gbl/RULE_LAUNCH_COMPILE.html). When this is not empty, CMake inserts it before the compilation command, essentially wrapping the compiler that would have been run with whatever `RULE_LAUNCH_COMPILE` contains. This works for the Unix Makefiles generator with all CMake versions from 2.8.0 onwards and with the Ninja generator for CMake 3.4 and later. All other CMake generators simply ignore `RULE_LAUNCH_COMPILE` and build the project normally. By setting `RULE_LAUNCH_COMPILE` to our `ccache` command, compilation is re-routed via ccache and build times decrease when rebuilding previously compiled sources with the same settings and source contents.

This global property should be set as early as possible, ideally before even the `project()` command is called, since `project()` performs checking on the compilers to be used. When the property setting is placed before `project()`, these checks will confirm that the compiler can be launched through `ccache` and report problems early. With this in mind, a recommended structure for the top level `CMakeLists.txt` file would be to start it like this:

```
cmake_minimum_required(VERSION 2.8)

find_program(CCACHE_PROGRAM ccache)
if(CCACHE_PROGRAM)
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif()

project(SomeProject)
```

The above will use `ccache` if it is available and fall back to normal non-ccache usage otherwise. Developers can opt-in simply by installing `ccache` and making it available on their PATH with no further setup required.

The studious developer may note that CMake also provides the `RULE_LAUNCH_LINK` global property which serves an analogous role for the linker. While it may be tempting to set this to route linker calls through ccache as well, there is no real benefit to doing so. This is because ccache doesn’t deal with link commands and will simply pass them through to the underlying linker anyway (this is [mentioned as a limitation](https://ccache.samba.org/) on the ccache website).

## Xcode

Developers could reasonably expect that it should be possible to use ccache with the Xcode generator too. Afterall, the underlying compiler is going to be GCC-compatible, so ccache should work just fine. The [CMake documentation](https://cmake.org/cmake/help/latest/prop_gbl/RULE_LAUNCH_COMPILE.html) for `RULE_LAUNCH_COMPILE` suggests we are out of luck though, stating the following:

> Other generators ignore this property because their underlying build systems provide no hook to wrap individual commands with a launcher.

Happily for us, this is not quite true for Xcode. While we cannot use `RULE_LAUNCH_COMPILE` with the Xcode generator directly, we can use the support for [CMAKE\_XCODE\_ATTRIBUTE\_…](https://cmake.org/cmake/help/latest/variable/CMAKE_XCODE_ATTRIBUTE_an-attribute.html) variables added in CMake 3.1 to achieve the same effect, albeit with a little help. When Xcode projects contain user-defined build settings with the names `CC` and `CXX`, they override what Xcode uses as the compilers for C and C++ sources respectively. As far as I can tell, these user-defined settings are not documented by Apple, but it is straightforward enough to verify that they have the effect described. All we then need to do is to create two small scripts (one for C and the other for C++) which redirects the compile command to `ccache` and use the `CC` and `CXX` attributes to tell Xcode about the scripts. Glossing over a few details for the moment, the script would be something like this (shown for C, replace `clang` with `clang++` for C++):

```
#!/bin/sh

exec ccache clang "$@"
```

Saving the scripts at the top of the source tree with names like `ccache-c` and `ccache-cxx`, the following lines can be added to the `CMakeLists.txt` file and that would be sufficient to get Xcode using ccache:

```
set(CMAKE_XCODE_ATTRIBUTE_CC  "${CMAKE_SOURCE_DIR}/ccache-c")
set(CMAKE_XCODE_ATTRIBUTE_CXX "${CMAKE_SOURCE_DIR}/ccache-cxx")
```

Annoyingly, it would appear that Xcode contains a bug related to how it chooses the linker when CC and CXX are defined. When building from within the Xcode IDE, setting CC and CXX results in the program specified for CC being used for linking as well, even for C++ projects. This results in linker errors because the C++ standard libraries are not included in the link. Oddly, building from the command line with `xcodebuild` yields different behaviour, with the `clang` or `clang++` executables being called directly rather than using either of the programs specified in CC or CXX. Programs do build successfully from the command line as a result, but the different behaviour is inconsistent. Thankfully, a simple workaround is to also define the analogous LD and LDPLUSPLUS variables for specifying the linkers. This causes the specified linkers to be used both within the Xcode IDE and when building from the command line with `xcodebuild`, so the behaviour is correct and consistent in both cases. The CMake syntax to achieve this is simply:

```
set(CMAKE_XCODE_ATTRIBUTE_LD         "${CMAKE_SOURCE_DIR}/ccache-c")
set(CMAKE_XCODE_ATTRIBUTE_LDPLUSPLUS "${CMAKE_SOURCE_DIR}/ccache-cxx")
```

Or if you don’t want to route linking via the launchers:

```
set(CMAKE_XCODE_ATTRIBUTE_LD         "${CMAKE_C_COMPILER}")
set(CMAKE_XCODE_ATTRIBUTE_LDPLUSPLUS "${CMAKE_CXX_COMPILER}")
```

## General implementation

The above explanation for Xcode glossed over a few details which should not be left unaddressed. The scripts contained hard-coded assumptions about where to find `ccache` and what underlying compiler to use. These are the sorts of things CMake is meant to handle for us more robustly. Indeed, we can do better by creating a pair of script template files and letting CMake populate tool paths for us. We can even make it general enough to support any compiler wrapper set in `RULE_LAUNCH_COMPILE`, not just ccache. First, create two files at the top of the source tree as follows:

*launch-c.in:*

```
#!/bin/sh

export CCACHE_CPP2=true
exec "${RULE_LAUNCH_COMPILE}" "${CMAKE_C_COMPILER}" "$@"
```

*launch-cxx.in:  
*

```
#!/bin/sh

export CCACHE_CPP2=true
exec "${RULE_LAUNCH_COMPILE}" "${CMAKE_CXX_COMPILER}" "$@"
```

Ignore the `CCACHE_CPP2` lines for now, we will come to that shortly. First, note how the `exec` command now uses the `RULE_LAUNCH_COMPILE` and `CMAKE_..._COMPILER` variables to specify the compiler wrapper (ccache in our case) and compiler to use. In `CMakeLists.txt`, the `configure_file()` command is used to copy these two script templates to the build directory, substituting the two variables along the way. Making these modifications and putting in the support for Unix Makefiles and Ninja as well, the `CMakeLists.txt` file looks like this:

```
cmake_minimum_required(VERSION 2.8)

find_program(CCACHE_PROGRAM ccache)
if(CCACHE_PROGRAM)
    # Support Unix Makefiles and Ninja
    set_property(GLOBAL PROPERTY RULE_LAUNCH_COMPILE "${CCACHE_PROGRAM}")
endif()

project(SomeProject)

get_property(RULE_LAUNCH_COMPILE GLOBAL PROPERTY RULE_LAUNCH_COMPILE)
if(RULE_LAUNCH_COMPILE AND CMAKE_GENERATOR STREQUAL "Xcode")
    # Set up wrapper scripts
    configure_file(launch-c.in launch-c)
    configure_file(launch-cxx.in launch-cxx)
    execute_process(COMMAND chmod a+rx
                             "${CMAKE_BINARY_DIR}/launch-c"
                             "${CMAKE_BINARY_DIR}/launch-cxx"
    )

    # Set Xcode project attributes to route compilation and linking
    # through our scripts
    set(CMAKE_XCODE_ATTRIBUTE_CC         "${CMAKE_BINARY_DIR}/launch-c")
    set(CMAKE_XCODE_ATTRIBUTE_CXX        "${CMAKE_BINARY_DIR}/launch-cxx")
    set(CMAKE_XCODE_ATTRIBUTE_LD         "${CMAKE_BINARY_DIR}/launch-c")
    set(CMAKE_XCODE_ATTRIBUTE_LDPLUSPLUS "${CMAKE_BINARY_DIR}/launch-cxx")
endif()
```

Note that the `project()` command comes *after* setting `RULE_LAUNCH_COMPILE` for Unix Makefiles and Ninja support, but *before* the calls to `configure_file()` to copy our launcher scripts. This is because we want CMake to work out the underlying C and C++ compilers, which is done by `project()`. If the `configure_file()` commands are put before `project()`, the `CMAKE_C_COMPILER` and `CMAKE_CXX_COMPILER` variables would not yet be set. Since Xcode can supply multiple toolchains, SDKs, etc., we should not simply assume `clang` can be found on the path, or indeed that the developer wants to use `clang` rather than `gcc` or some other compiler. The above arrangement still gives the developer the ability to select their compiler toolchain as before, even when cross-compiling to iOS, tvOS, etc. CMake will select the correct compiler and the re-routing scripts will use it rather than relying on some hard-coded location. A minor drawback is that the `project()` command is not testing the compiler through the launcher script when using Xcode, but the benefit of getting ccache working at all far outweighs that.

Returning to the scripts, they both contained the following line:

```
export CCACHE_CPP2=true
```

This is to handle certain pathalogical cases related to the preprocessor and enabling it is strongly recommended when using ccache with clang. Including this option may slightly increase build times for cache misses only (in the order of around 10%). The interested reader is directed to [this article](http://peter.eisentraut.org/blog/2014/12/01/ccache-and-clang-part-3/) for a more complete discussion of the subject.

## Improved functionality from CMake 3.4

From version 3.4, CMake also provides the [<LANG>\_COMPILER\_LAUNCHER](https://cmake.org/cmake/help/latest/prop_tgt/LANG_COMPILER_LAUNCHER.html) target properties (`<LANG>` may be `C` or `CXX`). The functionality is very similar to `RULE_LAUNCH_COMPILE`, but these properties can be set on a per-target basis and they also allow different launchers for different languages. If the same launchers should be used for all targets, then the [CMAKE\_<LANG>\_COMPILER\_LAUNCHER](https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_COMPILER_LAUNCHER.html) variables can be used to set the defaults for the corresponding target properties. Because the launchers can be language-specific, this is a better choice than `RULE_LAUNCH_COMPILE` if requiring CMake 3.4 or later is okay for your builds. The use of `RULE_LAUNCH_COMPILE` by projects is not recommended, as CMake expects to be able to use that for its own internal purposes in some situations.

For the most consistent behavior across all the CMake generators that support launchers, Ninja and Makefile generators can also be made to use the launcher scripts, as was done above for Xcode, rather than invoking ccache directly. Making this change, the launcher scripts and project file would then look something like this:

*launch-c.in:*

```
#!/bin/sh

# Xcode generator doesn't include the compiler as the
# first argument, Ninja and Makefiles do. Handle both cases.
if [[ "$1" = "${CMAKE_C_COMPILER}" ]] ; then
    shift
fi

export CCACHE_CPP2=true
exec "${C_LAUNCHER}" "${CMAKE_C_COMPILER}" "$@"
```

*launch-cxx.in:*

```
#!/bin/sh

# Xcode generator doesn't include the compiler as the
# first argument, Ninja and Makefiles do. Handle both cases.
if [[ "$1" = "${CMAKE_CXX_COMPILER}" ]] ; then
    shift
fi

export CCACHE_CPP2=true
exec "${CXX_LAUNCHER}" "${CMAKE_CXX_COMPILER}" "$@"
```

*CMakeLists.txt:*

```
cmake_minimum_required(VERSION 3.4)
project(SomeProject)

find_program(CCACHE_PROGRAM ccache)
if(CCACHE_PROGRAM)
    # Set up wrapper scripts
    set(C_LAUNCHER   "${CCACHE_PROGRAM}")
    set(CXX_LAUNCHER "${CCACHE_PROGRAM}")
    configure_file(launch-c.in   launch-c)
    configure_file(launch-cxx.in launch-cxx)
    execute_process(COMMAND chmod a+rx
                     "${CMAKE_BINARY_DIR}/launch-c"
                     "${CMAKE_BINARY_DIR}/launch-cxx"
    )

    if(CMAKE_GENERATOR STREQUAL "Xcode")
        # Set Xcode project attributes to route compilation and linking
        # through our scripts
        set(CMAKE_XCODE_ATTRIBUTE_CC         "${CMAKE_BINARY_DIR}/launch-c")
        set(CMAKE_XCODE_ATTRIBUTE_CXX        "${CMAKE_BINARY_DIR}/launch-cxx")
        set(CMAKE_XCODE_ATTRIBUTE_LD         "${CMAKE_BINARY_DIR}/launch-c")
        set(CMAKE_XCODE_ATTRIBUTE_LDPLUSPLUS "${CMAKE_BINARY_DIR}/launch-cxx")
    else()
        # Support Unix Makefiles and Ninja
        set(CMAKE_C_COMPILER_LAUNCHER   "${CMAKE_BINARY_DIR}/launch-c")
        set(CMAKE_CXX_COMPILER_LAUNCHER "${CMAKE_BINARY_DIR}/launch-cxx")
    endif()
 endif()
```

All three generators now behave consistently, using the same language-specific launch scripts. The above example places all of the ccache-specific logic after the `project()` command, so it could easily be factored out into a separate file and brought in with an `include()` or similar. The `project()` command won’t perform its compiler and linker tests with the launchers now that `RULE_LAUNCH_COMPILE` isn’t being set before `project()` is called, only the real underlying compilers will be tested by `project()`. This is a minor loss which only affects the Ninja and Makefiles generators and one could argue the consistency in behaviour across all generators is a fair tradeoff.

## Acknowledgements

Credit to [Peter Steinberger](https://pspdfkit.com/blog/2015/ccache-for-fun-and-profit/) for highlighting the technique of setting `CC` and `CXX` in Xcode project files to override the compiler used. His article also contains a few other useful observations for using ccache with clang which may be of interest to some readers.

---

![](https://crascit.com/wp-content/uploads/2019/08/CraigCasualPortrait_374x512.png)

![](https://crascit.com/wp-content/uploads/2018/08/front-cover-794x1123.jpg)