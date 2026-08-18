---
title: "Deferred rendering vs Forward+ rendering in AAA games."
source: "https://www.reddit.com/r/GraphicsProgramming/comments/1kmrura/deferred_rendering_vs_forward_rendering_in_aaa/?chainedPosts=t3_1bzslrv"
author:
  - "[[jbl271]]"
published: 2025-05-15
created: 2025-11-04
description:
tags:
  - "clippings"
---
So, I’ve been working on a hobby renderer for the past few months, and right now I’m trying to implement deferred rendering. This made me wonder how relevant deferred rendering is these days, since, to me at least, it seems kinda old. Then I discovered that there’s a variation on forward rendering called forward+, volume tiled forward+, or whatever other names they have for it. These new forward rendering variations seemed to have solved the light culling issue that typical forward rendering suffers from, and this is also something that deferred rendering solves as well, so it would seem to me that forward+ would be a pretty good choice over deferred, especially since you can’t do transparency in a deferred pipeline. To my surprise however, it seems that most AAA studios still prefer to use deferred rendering over forward+ (or whatever it’s called). Why is that?

---

## Comments

> **hanotak** • [42 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mscm93e/) •
> 
> I support both in my engine, but I've found deferred to be generally faster (I use clustered lighting for both). For me, it's primarily because other effects already need parts of the g-buffer (SSAO needs depths and normals, for example). Because of that, forward rendering ends up just being "deferred-lite", but with a second geometry pass (pre-pass to get depths and normals, then forward pass). Even with the savings from using early z-out in the fragment shader, just doing full deferred with a single geometry pass seems faster.
> 
> Of course, on GPUs with less memory bandwidth, this may be different.
> 
> You will also already generally have a separate pass anyway for transparent materials, since they need to be treated differently with regard to depth testing.
> 
> In deferred mode, my renderer does a pre pass (depths, normals, albedo, emissive, metallic, roughness), then a full screen quad for deferred shading, then a forward pass for transparencies.
> 
> In forward mode, it does a pre-pass for just depths and normals, then a forward opaque pass, and a forward transparent pass.
> 
> > **jbl271** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msd8ofa/) •
> > 
> > Yeah that’s a good point, that a lot of effects seem to already be in screen space so maybe defaulting to deferred seems like a pretty convenient approach.
> > 
> > **Lord\_Zane** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mspavgi/) •
> > 
> > I work on rendering for an open source game engine [https://bevyengine.org](https://bevyengine.org/), and we found generally the same results (on desktop) as you.
> > 
> > We have a number of different render paths:
> > 
> > 1. Forward
> > 2. Forward with optional {depth, normal, motion vector} prepasses (e.g. SSAO needs just depth + normal, TAA needs just MV + depth)
> > 3. Deferred, with or without motion vectors as an extra attachment
> > 4. Visbuffer -> forward shading (virtual geometry only)
> > 5. Visbuffer -> gbuffer -> deferred shading (virtual geometry only)
> > 
> > All methods use CPU-based light clustering, you can mix and match the modes and render different objects in different ways, and on supported (non-webgl2) platforms, if you're using deferred, a depth prepass (iirc), or virtual geometry, you can use 2 pass occlusion culling.
> > 
> > We found that typically deferred is the cheapest once you plan on using anything like SSAO that needs extra data besides screen color. The prepass in forward was generally not worth it.
> > 
> > You could do a hybrid where you render depth only for 2 pass occlusion culling, and then render fully forward after that, but at this point I think you would be better off going with a visbuffer.
> > 
> > Imo visbuffer in general is great purely for ergonomics, but you can't go wrong with deferred either.
> > 
> > **Ty\_Rymer** • [\-1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msex0j4/) •
> > 
> > why not do a depth only prepass for either, and then have all the material values only calculated in a geometry pass?
> > 
> > so deferred would be: depth prepass, depth culled gbuffer pass, deferred lighting pass,
> > 
> > forward would be: depth prepass, depth culled forward pass that also outputs normals and other metadata

> **FoxCanFly** • [27 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mscrnet/) •
> 
> The most modern approach is Visibility Buffer instead of forward or deffered. It saves memory bandwidth almost as forward and solves its problems (poor quad occupancy, complex shaders, effects requiring a g-buffer) like deffered one
> 
> > **tamat** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msetjuk/) •
> > 
> > all Visibility Buffer engines I've seen do that to generate the GBuffers for deferred.
> > 
> > **jbl271** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msd8qx5/) •
> > 
> > What’s a visibility buffer? Could you explain it a little more?
> > 
> > > **hanotak** • [10 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msdhs3e/) •
> > > 
> > > [http://filmicworlds.com/blog/visibility-buffer-rendering-with-material-graphs/](http://filmicworlds.com/blog/visibility-buffer-rendering-with-material-graphs/)
> > > 
> > > The idea is to rasterize as little data as possible (just triangle id, even) in order to minimize the amount of time spent on fragment shader invocations that get thrown away due to poor quad utilization.
> 
> **Plazmatic** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mse39io/) •
> 
> How does this deal with MSAA? That effectively eliminates the overdraw problem doesn't it? Because now the overdraw *is what you wanted to do* in the first place? Which then flips everything back to one of the other ones being the best, because that extra 2x2 cost is no longer "extra".
> 
> > **shadowndacorner** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mse7d6i/) •
> > 
> > > How does this deal with MSAA?
> > 
> > [Fantastically if you're smart about how you implement it](http://filmicworlds.com/blog/decoupled-visibility-multisampling/).
> > 
> > > That effectively eliminates the overdraw problem doesn't it?
> > 
> > It improves it significantly, but it doesn't "solve" it any more than deferred or a z prepass does. There really aren't any scenarios in which you *want* overdraw - it's always unnecessary work.
> > 
> > > Which then flips everything back to one of the other ones being the best
> > 
> > I'm not sure what you mean by this. Are the "other ones" forward and deferred? If so, vbuffer rendering tends to be faster than forward or deferred with high triangle density, but the trade off is a significant bump in implementation complexity because you need to compute all derivatives yourself. If you don't need the perf benefits of vbuffers or don't want to manage that complexity, deferred has *most* of the same benefits, but it's significantly less flexible and is slower for small triangles. Clustered forward is king for simple scenes, but these days, isn't better at much else, especially if you want to use a deferred-like post effect pipeline. You can, ofc, run your "post processing" in the fragment shader if you're clever about it, but that's clunky as hell.

> **keelanstuart** • [9 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msdhv9w/) •
> 
> I have implemented forward and deferred pipelines... I prefer deferred because you generate rich metadata that you can use elsewhere. Also, bandwidth issues are rare these days unless you're talking mobile (and I don't care about that)... even integrated Intel graphics are decent enough to push that kind of data.
> 
> > **susosusosuso** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msensfi/) •
> > 
> > Actually mobile gpus are even better than desktop gpus in deferred because it maps the hardware better
> > 
> > **robbertzzz1** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msgups5/) •
> > 
> > > even integrated Intel graphics are decent enough
> > 
> > Totally unrelated, but when I bought a new laptop with a high end Intel CPU earlier this year I was very surprised to learn that the integrated GPU supports ray tracing.
> > 
> > > **keelanstuart** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msgzpoa/) •
> > > 
> > > Yeah, I think that just proves my point... I used to think of integrated Intel graphics as the absolute bottom of the performance heap (and they may actually still *be* that, given the relative performance of other contemporaries), but for most people here doing hobbyist engines or learning ray tracing techniques, they're more than sufficient.

> **PixelsGoBoom** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msehdfi/) •
> 
> Not a graphics engineer, but transparency will always be a separate pass regardless.
> 
> You first draw your opaque geometry which you would render front to back, transparencies after which you would render back to front.
> 
> > **SirLynix** • [5 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msehsjg/) •
> > 
> > Drawing opaque geometry front to back is inefficient because it breaks batching (and forces GPU states and pipelines to be set more than once), better use a depth pass to fill thé depth buffer first.

> **MegaCockInhaler** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msd25n8/) •
> 
> Forward tends to be faster but you are also a bit more limited. Deferred scales extremely well with lots of lights. But if you look at the new Doom games, they all use clustered forward rendering, look gorgeous and perform very well so that’s a good example of how to do it right. There’s a lot of rendering features that work better/easier on deferred. If you are doing mobile games you almost certainly will be doing forward rendering
> 
> > **jbl271** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msdaza9/) •
> > 
> > Yeah I figured deferred would be a no go on mobile since they’re limited on their VRAM.
> > 
> > **Icy\_Curry** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mxiphh7/) •
> > 
> > Wait. The newer Doom games don't use deferred rendering? So we can still use driver forms of AA like MSAA and sparse grid supersampling AA (SGSSAA), etc. with them, like we can with older games, since the newer Doom games don't use deferred rendering? Are you sure?

> **andr3wmac** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mscmjs3/) •
> 
> Convenience.
> 
> Even with Forward+ you're not generating a full g-buffer, which means a lot of techniques that were developed for deferred have to be reworked. Is it possible? Yes, but unless you have a specific reason to not use deferred it just comes back to why not go with the path of least resistance? It's a very tempting path because you can do so much with such ease when you're just running a quad over the screen and sampling the g-buffer.
> 
> Arguably, the only advantages left to forward are mobile performance and MSAA. Unfortunately when TAA emerged as a technique for anti-aliasing in deferred it brought with it the opportunity to do more stochastic techniques and let TAA sort it out, so we're now getting even more entrenched.
> 
> > **jbl271** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msdakl9/) •
> > 
> > I haven’t implemented TAA yet nor do I really know what the algorithm is I’ve just know it exists from playing games, but what do people think of MSAA vs TAA?

> **trad\_emark** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msez32a/) •
> 
> A case for forward: It is simpler to get going (half the work of deferred). It is simpler to write shaders for custom effects (no limit on what to put in the g-buffer).

> **LordDarthShader** • [0 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mscrazk/) •
> 
> I thought the industry moved to compute rendering, like just doing a lite G buffer on the raster/pixel shader and doing all the clustered light calculations in the compute shader. Is this still true?
> 
> > **jbl271** • [4 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msdassh/) •
> > 
> > As far as I’m aware, most AAA engines default to a deferred rendering pipeline, but someone more knowledgeable probably knows better than I do.

> **Ty\_Rymer** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msewldt/) •
> 
> visibility buffers is kindah the next step for deferred

> **TheLondoneer** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/mseicl6/) •
> 
> [https://youtu.be/QVbOp1h-Jb4?si=OP3phzpGz1Dovzmt](https://youtu.be/QVbOp1h-Jb4?si=OP3phzpGz1Dovzmt)

> **WelpIamoutofideas** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1kmrura/comment/msqj8ba/) •
> 
> I'm going to throw my two cents on the table. I'm not in the game industry professionally and I haven't released a full game so take this with a grain of salt
> 
> Doom Eternal (I assume dark ages as well) uses Clustered forward completely for lighting, with almost no lightmaps at all in use, and it is one of the most optimized games for its time and even better today.
> 
> People have made comments saying that even forward needs a separate pass for transparent geometry. This is true but completely misses the point when people use transparency as a downside.
> 
> Transparency in deferred rendering requires a complete forward renderer to implement. You have to write that forward renderer anyway. It's probably not going to be as good as if you had spent your full-time on it. It'll mean doubling work on shaders in certain circumstances. Forward rendering can use the exact same rendering infrastructure, You just invert the sorting criteria.
> 
> Deferred rendering also allows you to more easily change lighting models within a scene. With deferred rendering, there's very limited options. If you want to say, have cartoony pickups with a more realistic environment like Doom Eternal. You either have to use the stencil buffer to selectively choose different shading modes, A separate material buffer to do exactly the same thing, or, you render it in passes.
> 
> On the other side, deferred makes decals with material properties on surfaces piss easy. You just slap the decal on along with any other surface information, say normals, emissivity, etc. Forward requires a little bit more work to do that.
> 
> Depending on what you're targeting, you also might not have a choice. You can't use TAA in VR, it'll make people motion sick. Especially with mobile processors running in VR headsets nowadays. You are definitely better off in that area if you're thinking about mobile or VR.