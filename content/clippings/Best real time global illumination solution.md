---
title: Best real time global illumination solution?
source: https://www.reddit.com/r/GraphicsProgramming/comments/1lo5afk/best_real_time_global_illumination_solution/
author:
  - "[[The_Not_Bob]]"
published: 2025-06-30
created: 2025-09-21
description:
tags:
  - clippings
  - global-illumination
---
In your opinion what is the best real time global illumination solution. I'm looking for the best global illumination solution for the game engine I am building.

I have looked a bit into ddgi, Virtual point lights and vxgi. I like these solutions and might implement any of them but I was really looking for a solution that nativky supported reflections (because I hate SSR and want something more dynamic than prebaked cubemaps) but it seems like the only option would be full on raytracing. I'm not sure if there is any viable raytracing solution (with reflections) that would ask work on lower end hardware.

I'd be happy to know about any other global illumination solutions you think are better even if they don't include reflections. Or other methods for reflections that are dynamic and not screen space. 🥐

---

## Comments

> **SpudroSpaerde** • [40 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0k827m/) •
> 
> One of my main takeaways from REAC 2025 was that your GI solution is highly dependent on your game's requirements, target hardware and artist workflows. There is currently no consensus on what the best solution looks like at least as far as I can tell.
> 
> track me

> **Fit\_Paint\_3823** • [26 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0kcgx1/) •
> 
> meta prediction: I think the games that are not unreal based or have some elite graphics programmers there who can code entirely bespoke (and full of state of the art novelty) solutions for their games will heavily trend towards a DDGI style GI, meaning, you have a probe grid like the ones that have existed for 20 years, just update them with ray tracing and each probe has an additional depth buffer to deal with light leakage a bit better than we were used to. you focuse on diffuse and do specular in a different way or not dynamically at all (e.g. just via old school env maps per area supplemented by SSR).
> 
> this is because that approach is relatively simple (well, as far as GI systems go), and scales pretty well to a wide variety of different content types. while having pretty decent performance at least if you work with a reasonable minspec (like ps5-level hardware). but it's far from the highest quality possible and has plenty of issues. leaking is not completely solved, updates have to be low frequency so that will cause issues, memory usage is not trivial etc.
> 
> > **shadowndacorner** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0mfn04/) •
> > 
> > Just to add onto your prediction, DDGI is also a nice foundation for adding screen probes later on like GI 1.0, Lumen, or GIBS (where the latter is obviously pretty different than the other two, but follows the same idea of "spawn probes on opaque geometry by hole filling coverage on the g buffer"). You need world space probes for transparent objects at minimum, and aside from that, it gives a better baseline when eg rapidly turning than falling back to nothing.
> > 
> > The other nice thing about DDGI is that if hardware RT isn't available, it's pretty trivial to get a low-ish quality fallback with pure RSMs, then a decent quality fallback with RSM + SDFs for occlusion testing. You lose out on accurate multi bounce GI this way, but you can do something like Radiance Hints' approach to exchanging energy between probes to approximate it.
> > 
> > > **Pawan4321** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n4vwpw6/) •
> > > 
> > > Would you mind elaborating a bit on how you would use RSMs to update the DDGI probes?
> > > 
> > > > **shadowndacorner** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n4wtlzv/) •
> > > > 
> > > > You just treat a subset of the RSM samples as if they're ray hits rather than using RT. Ideally you'd at least have SDF traces for the depth function (which you can then use as an approximate visibility test for the RSM samples), but even better is to do an SDF trace for each sample to prevent light leaks.
> > > > 
> > > > You only get single bounce this way ofc, but it's a reasonable fallback on low end imo.
> > > > 
> > > > > **Pawan4321** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n4x078h/) •
> > > > > 
> > > > > Ok, that makes sense. Awesome, thanks!
> 
> **susosusosuso** • [0 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0kzj2w/) •
> 
> Do you mean ssgi?
> 
> > **skatehumor** • [6 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0lhxw8/) •
> > 
> > The approach described here seems more like DDGI, though more specifically, DDGI tends to describe a more recent probe-based technique that leverages ray tracing and is entirely done at runtime.
> > 
> > Probe-based techniques do go back a long way, but usually in the context of baked lighting solutions.

> **shadowndacorner** • [8 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0mivhr/) •
> 
> The "best" global illumination solution is path tracing. It's also the most expensive, so we can't really do it generally yet. So the "best" solution *for now* is whatever looks best for your game content that runs well on your target hardware. Whether that is a voxel based system, hardware RT, etc is entirely dependent on your context.
> 
> Re: reflections, one thing to note about DDGI is that if you represent them as SH's rather than octahedral textures, you can theoretically use the tricks from either Halo 3 or Star Wars Battlefront 2 for a reasonable specular contribution as well. This is not as good as real reflections, but can be pretty decent for rough surfaces. Halo 3's trick is more fundamentally solid imo, but the BF2 trick is dead simple and has pretty good results.
> 
> For accurate reflections, you really need some form of ray tracing, whether it's software RT like Lumen's SDF mode, or hardware RT. VCT (which *does* support reflections and runs well on today's low end hardware) is quite a bit faster (especially for rough surfaces, assuming you actually do an approximation of cone tracing), but it's pretty lossy unless you go pretty high resolution.
> 
> If you're willing to do hardware RT, imo the best approach is more or less the Battlefield V approach - run stochastic SSR against your g buffer (crucially reshading rather than sampling from the previous frame) and only do hardware tracing on disocclusion. You can do a similar fallback to eg VCT, but that doesn't tend to integrate *nearly* as cleanly imo.

> **Silent-Selection8161** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0mu71e/) •
> 
> Here's a low end hardware solution with reflections: [https://gpuopen.com/fidelityfx-brixelizer/](https://gpuopen.com/fidelityfx-brixelizer/)
> 
> You'll have to hack in your ability to read meshes into the GI texture cache without viewing them first, that's should be coming with the second version of this thing but IDK when that's out. Otherwise, this is about as low end as it gets with reflections that aren't an absolute pain that require an entire studio of artists to work through.

> **NoImprovement4668** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1lo5afk/comment/n0s9f2t/) •
> 
> cool this sounds similar to one of my questions few days ago, i personally use virtual point lights (VPLs), subdivide the mesh at runtime and then in tesselation shaders themself calculate the vpl per vertex as to not do per pixel (on my engine i get ~200 fps with this technique with 1024 vpls vs 25 fps doing per pixel) and this helps with optimization a lot and it looks really nice without worrying about complex things like lightmap uvs or having to deal with raytracing