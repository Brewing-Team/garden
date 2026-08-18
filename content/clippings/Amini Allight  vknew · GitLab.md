---
title: "Amini Allight / vknew · GitLab"
source: "https://gitlab.com/amini-allight/vknew"
author:
  - "[[GitLab]]"
published: 2025-03-22
created: 2025-09-26
description: "An example of modern Vulkan with descriptor indexing, dynamic rendering and shader objects."
tags:
  - "clippings"
---
Select Git revision

- Selected
- master default protected

1 result

- Open with
	- Visual Studio Code
		[SSH](https://vscode.git/clone?url=git%40gitlab.com%3Aamini-allight%2Fvknew.git) [HTTPS](https://vscode.git/clone?url=https%3A%2F%2Fgitlab.com%2Famini-allight%2Fvknew.git)
	- IntelliJ IDEA
		[SSH](https://gitlab.com/amini-allight/checkout/git?idea.required.plugins.id=Git4Idea&checkout.repo=git%40gitlab.com%3Aamini-allight%2Fvknew.git) [HTTPS](https://gitlab.com/amini-allight/checkout/git?idea.required.plugins.id=Git4Idea&checkout.repo=https%3A%2F%2Fgitlab.com%2Famini-allight%2Fvknew.git)
- Download source code

- Your workspaces
	A workspace is a virtual sandbox environment for your code in GitLab.
	No agents available to create workspaces. Please consult [Workspaces documentation](https://gitlab.com/help/user/workspace/workspaces_troubleshooting.html) for troubleshooting.

[removed unnecessary and unused reference to VkFramebuffer](https://gitlab.com/amini-allight/vknew/-/commit/a490c3218af96307d018ff07c66f491a1287689d)

[Amini Allight](https://gitlab.com/amini-allight) authored

a490c321

[History](https://gitlab.com/amini-allight/vknew/-/commits/master?ref_type=HEADS)

[a490c321](https://gitlab.com/amini-allight/vknew/-/commit/a490c3218af96307d018ff07c66f491a1287689d)

[History](https://gitlab.com/amini-allight/vknew/-/commits/master?ref_type=HEADS)

| Name | Last commit | Last update |
| --- | --- | --- |
| [shaders](https://gitlab.com/amini-allight/vknew/-/tree/master/shaders?ref_type=heads "shaders") |  |  |
| [src](https://gitlab.com/amini-allight/vknew/-/tree/master/src?ref_type=heads "src") |  |  |
| [.gitignore](https://gitlab.com/amini-allight/vknew/-/blob/master/.gitignore?ref_type=heads ".gitignore") |  |  |
| [CMakeLists.txt](https://gitlab.com/amini-allight/vknew/-/blob/master/CMakeLists.txt?ref_type=heads "CMakeLists.txt") |  |  |
| [license](https://gitlab.com/amini-allight/vknew/-/blob/master/license?ref_type=heads "license") |  |  |
| [readme.md](https://gitlab.com/amini-allight/vknew/-/blob/master/readme.md?ref_type=heads "readme.md") |  |  |

[**readme.md**](https://gitlab.com/amini-allight/vknew/-/blob/master/readme.md?ref_type=heads)

## vknew: Modern Vulkan with descriptor indexing, dynamic rendering and shader objects

This is the source code for my [modern Vulkan with descriptor indexing, dynamic rendering and shader objects tutorial](https://amini-allight.org/post/vknew-modern-vulkan-with-descriptor-indexing-dynamic-rendering-and-shader-objects).

## Dependencies

- glslangValidator (only required for build)
- SDL2
- Vulkan (version 1.3+ with the `VK_EXT_shader_object` extension)

## Usage

Build the application with:

```shell
mkdir -p build

cd build

cmake ..

make -j$(nproc)
```

Then run it with:

```shell
cd bin

./vknew
```

A window should appear featuring a number of checkered squares.

## License

Created by Amini Allight. The contents of this repository are licensed under Creative Commons Zero (CC0 1.0), placing them in the public domain.

The one exception to this is the file `vk_mem_alloc.h` taken from AMD's [Vulkan Memory Allocator](https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator) project, the license details of which can be found in the header of that same file.

This tutorial is not affiliated with or endorsed by the Khronos Group.