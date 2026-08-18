---
title: Voxel cone-traced global illumination in OpenGL
source: https://www.reddit.com/r/GraphicsProgramming/comments/1ohh7au/voxel_conetraced_global_illumination_in_opengl/
author:
  - "[[cranuses]]"
published: 2025-10-27
created: 2025-10-28
description: Reddit is where millions of people gather for conversations about the things they care about, in over 100,000 subreddit communities.
tags:
  - clippings
  - global-illumination
  - voxel
  - graphics
---
GitHub (vxgi-dev branch, still cleaning up; in my testing only works on linux, fuck msvc): [https://github.com/Jan-Stangelj/glrhi](https://github.com/Jan-Stangelj/glrhi)

Usefoul resources:  
[https://jose-villegas.github.io/post/deferred\_voxel\_shading/](https://jose-villegas.github.io/post/deferred_voxel_shading/)

[https://wickedengine.net/2017/08/voxel-based-global-illumination/comment-page-1/](https://wickedengine.net/2017/08/voxel-based-global-illumination/comment-page-1/)

[https://developer.nvidia.com/content/basics-gpu-voxelization](https://developer.nvidia.com/content/basics-gpu-voxelization)

[https://developer.nvidia.com/gpugems/gpugems2/part-v-image-oriented-computing/chapter-42-conservative-rasterization](https://developer.nvidia.com/gpugems/gpugems2/part-v-image-oriented-computing/chapter-42-conservative-rasterization)

---

## Comments

> **0bexx** • [14 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlnx9ic/) •
> 
> you should add an GI intensity multiplier because the GI is beautiful but it’s hard to see. i think the intensity of the direct light is disproportionate to the indirect light
> 
> > **shadowndacorner** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlp4bp4/) •
> > 
> > Disagree. I'd rather have something that looks physically correct than something super exaggerated. This looks like quite a good implementation!
> > 
> > > **susosusosuso** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlp4izl/) •
> > > 
> > > This. Don’t fake it.. try to see why it’s wrong
> > > 
> > > **0bexx** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlp57ua/) •
> > > 
> > > maybe cycles is just super opinionated, but this looks absolutely nothing like the (physically correct) path traced result. the GI implementation is absolutely beautiful (from what i can see) but is definitely disproportionate to the direct light. maybe there is something about this stack i’m unaware of.

> **shadowndacorner** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlp5q6s/) •
> 
> It looks like you need some post processing (esp bloom/tone mapping), but it looks like quite a good implementation of VCT. From quickly skimming the code, it looks like you're doing a uniform grid for voxel storage - what's the resolution of the grid used here?
> 
> Anything weird/interesting about your implementation?
> 
> > **cranuses** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlpfnj1/) •
> > 
> > I cranked the sun intensity way up, so the GI would be more noticable. Otherwise im using PBRneutral.

> **cranuses** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1ohh7au/comment/nlpfgp7/) •
> 
> Turns out the renderer had some major bugs despite looking good enough. Firstly, for the direct lighting voxel texture i was using the camera position for the lambertian instead of the normal. And secendly, the voxel normals werent encoded correctly. I will probally upload some new pics tomorrow.