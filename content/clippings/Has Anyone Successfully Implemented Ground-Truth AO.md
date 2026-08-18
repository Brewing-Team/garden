---
title: "Has Anyone Successfully Implemented Ground-Truth AO?"
source: "https://www.reddit.com/r/opengl/comments/96api8/has_anyone_successfully_implemented_groundtruth_ao/"
author:
  - "[[FlexMasterPeemo]]"
published: 2018-08-10
created: 2025-09-21
description:
tags:
  - "clippings"
---
Hey guys, I'm having some troubles implementing GTAO based on [this](http://iryoku.com/downloads/Practical-Realtime-Strategies-for-Accurate-Indirect-Occlusion.pdf) paper in GLSL. I saw that Blender's Eevee renderer uses it so I took a look at its source code but it's pretty confusing to look through haha. Anyone has a working implementation that are willing to share or show off? Really want to get it working because out of all existing AO techniques it seems like this one is superior in quality.

---

## Comments

> **Kvaleya** • [8 points](https://reddit.com/r/opengl/comments/96api8/comment/e3z4xe6/) •
> 
> I've successfully implemented it, but I followed the slides from siggraph instead of the paper. The link to the slides can be found [here](http://blog.selfshadow.com/publications/s2016-shading-course/).
> 
> Thing is I wrote the shader a year ago and I've also optimized it somewhat, so it's not very readable at this point. I'll have a look at it in the morning, I'll need to (re)use it soon for my new engine/renderer anyway.
> 
> track me
> 
> > **FlexMasterPeemo** • [4 points](https://reddit.com/r/opengl/comments/96api8/comment/e3z6viz/) •
> > 
> > Yeah I'm following the slides too (I forgot to link them in the OP), they go into more detail than the paper does.
> > 
> > Optimization is a blessing and a curse sometimes...
> > 
> > > **Kvaleya** • [7 points](https://reddit.com/r/opengl/comments/96api8/comment/e40d2ie/) •
> > > 
> > > [Here](https://pastebin.com/bKxFnN5i) is the shader source code. It is almost usable as-is, all you need to do is set the proper uniforms and remove the last remaining *#include*. I've also added comments and removed microoptimizations. I think they didn't really make any difference...
> > > 
> > > Hope that this will be helpful, but I don't know if it is any better than the source you've already been following.
> > > 
> > > [Screenshots](https://imgur.com/a/RfrYmOO)
> > > 
> > > I've noticed that there is a certain flaw in the shader (see comments in GetCameraVec) that makes the AO world-space radius dependent on FOV. The greater the FOV, the greater the AO radius is. However it should be an easy fix and it works reasonably well with common FOVs anyway.
> > > 
> > > Also here is the [temporal filtering shader](https://pastebin.com/vjGsCqaH) I use to filter the noisy output of the first shader.
> > > 
> > > > **FlexMasterPeemo** • [2 points](https://reddit.com/r/opengl/comments/96api8/comment/e415l90/) •
> > > > 
> > > > Wow! That is a huge help man! If you're alright with it, I'll adapt some of my code to work properly (I'll of course credit you appropriately) I've been stuck with this for quite some time now... Again, huge thanks for coming through!
> > > > 
> > > > > **Kvaleya** • [2 points](https://reddit.com/r/opengl/comments/96api8/comment/e42tevh/) •
> > > > > 
> > > > > No problem, feel free to use it however you like.
> > > > > 
> > > > > > **DubScoutMusic** • [1 points](https://reddit.com/r/opengl/comments/96api8/comment/e48f6ae/) •
> > > > > > 
> > > > > > Thanks very much for sharing this code!
> > > > > > 
> > > > > > I'm working on my own implementation right now, and I'm struggling with the temporal blending - would it be possible to share your temporal shader?
> > > > > > 
> > > > > > > **Kvaleya** • [2 points](https://reddit.com/r/opengl/comments/96api8/comment/e48jeo1/) •
> > > > > > > 
> > > > > > > I've updated the original comment with a link to the temporal shader source to keep the links in one place.
> > > > > > > 
> > > > > > > > **DubScoutMusic** • [1 points](https://reddit.com/r/opengl/comments/96api8/comment/e48qh2n/) •
> > > > > > > > 
> > > > > > > > Thanks very much!