---
title: Direct Lighting with Sparse Voxel Octrees
source: https://www.leadwerks.com/community/blogs/entry/2741-direct-lighting-with-sparse-voxel-octrees/
author:
  - "[[Josh]]"
published: 1970-01-01
created: 2025-10-16
description: "Previously I described how I was able to save the voxel data into a sparse octree and correctly lookup the right voxel in a shader. This shot shows that each triangle is being rasterized separately, i.e. the triangle bounding box is being correctly trimmed to avoid a lot of overlapping voxels: Ca..."
tags:
  - clippings
  - global-illumination
  - voxel
  - octree
---
[Jump to content](https://www.leadwerks.com/community/blogs/entry/2741-direct-lighting-with-sparse-voxel-octrees/#ipsLayout_mainArea "Go to main content on this page")

- [Sign In](https://www.leadwerks.com/community/login/)

Previously I described how I was able to save the voxel data into a sparse octree and correctly lookup the right voxel in a shader. This shot shows that each triangle is being rasterized separately, i.e. the triangle bounding box is being correctly trimmed to avoid a lot of overlapping voxels:

[![vox.thumb.png.414a8a4812831567dfbd4c0428849824.png](https://leadwerksstorage.s3.us-east-2.amazonaws.com/monthly_2022_01/vox.thumb.png.414a8a4812831567dfbd4c0428849824.png)](https://leadwerksstorage.s3.us-east-2.amazonaws.com/monthly_2022_01/vox.png.7b256a064200e5fc732d5272be996a8d.png)

Calculating direct lighting using the sparse octree was very difficult, and took me several days of debugging. I'm not 100% sure what the problem was, other than it seems GLSL code is not quite as flexible as C++. I actually had the same exact function working in GLSL and C++, and it worked perfectly in C++ but gave wrong results in GLSL! Of course I did not have a debugger for my GLSL code, so I ended up having to write a lot of if statements and outputting a pixel color base on the result. In the end I finally tracked the problem down to some data stored in an array, changed the way the routine worked, but what the exact issue was I'll never know.

With the sparse voxel octree, we only have about 400,000 pixels to draw when we process direct lighting. Rendering all voxels in a 256x256x256 volume texture would require 16 million pixels to be drawn. So the sparse approach requires us to draw only 2% the number of pixels we would have to otherwise. Using shadow maps, on a 1920x1080 screen we would have to calculate about 2,000,000 shadow intersections. Although we are not comparing the same exact things, this does make me optimistic for the final performance results. Basically, instead of calculating shadow visibility for each pixels, we can just calculate per voxel, and your voxels are always going to be quite a bit bigger than screen pixels. So the whole issue of balancing shadow map resolution with screen resolution goes away.

Ray traversal is very fast because it skips large chunks of empty space, instead of checking every single grid space for a voxel.

The voxel resolution below is not very high, I am only using one octree, and there's currently no blending / filtering, but that will all come in time.

[![Untitled.thumb.png.669fa5e8265b96b49c880b4f8895c570.png](https://leadwerksstorage.s3.us-east-2.amazonaws.com/monthly_2022_01/Untitled.thumb.png.669fa5e8265b96b49c880b4f8895c570.png)](https://leadwerksstorage.s3.us-east-2.amazonaws.com/monthly_2022_01/Untitled.png.0e381243874ae16e886063384dc1377b.png)

Leadwerks 1 and 3D World Studio used lightmaps for lighting. Later versions of Leadwerks used deferred lighting and shadowmaps. Being able to roll out another cutting-edge lighting technology in Ultra Engine is icing on the cake for the new engine. I expect this will allow particle shadows and transparent glass with colored shadows, as well as real-time global illumination and reflections, all with great performance on most hardware.

- 3