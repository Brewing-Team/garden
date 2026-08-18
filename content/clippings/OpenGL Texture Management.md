---
title: "OpenGL Texture Management"
source: "https://www.reddit.com/r/GraphicsProgramming/comments/1ojfw3p/opengl_texture_management/"
author:
  - "[[sansisalvo3434]]"
published: 2025-10-29
created: 2025-11-02
description: "Reddit is where millions of people gather for conversations about the things they care about, in over 100,000 subreddit communities."
tags:
  - "clippings"
  - "opengl"
  - "game-engine"
---
Hi, I am currently writing a 3D game engine and learning advanced OpenGL techniques. I am having trouble with texture loading.

I've tried bindless textures, but this method allocates a lot of memory during initialization, But we can manage by removing the unused ones and reloading them.

Another approach I tried was texture arrays. Conceptually, these are not the same thing, but anyway, I have a problem with texture arrays: resolution mismatch. For example, we have to use the same mip level and resolution, etc., but the actual problem is that the textures can be different sizes or mip levels. We have to manage the memory and specify a size for all the textures.

I've also heard of "sparse bindless texture arrays."

There are also some optimization methods, like compressed formats.

But first, I want to learn how to manage my texture loading pipeline before moving on to PBR lighting.

Is there an efficient, modern approach to doing that?

---

## Comments

> **track33r** • [6 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm2ykit/) •
> 
> Why do you have impression that there are different memory footprints depending on bundles technique?
> 
> > **sansisalvo3434** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm5e3vl/) •
> > 
> > Actually, that's a good question. While I'm using bindless textures, the compile-time performance becomes pretty bad, probably because it loads all the textures at once. For now, i am using a single thread. Despite using indirect rendering, it had poor performance.
> > 
> > So, what confuses me is whether bindless textures are enough to manage all the textures or if I should mix them with other things.
> > 
> > Thanks!
> > 
> > > **track33r** • [6 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm5ep7g/) •
> > > 
> > > Compile time has nothing to do with loading textures because it happens in runtime.

> **corysama** • [5 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm3h2m3/) •
> 
> Definitely use compressed textures. [https://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/](https://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/) Use BC6/7 for most everything. BC1 for when you really need to squeeze.
> 
> Don't worry about sparse arrays. They work great on consoles. But, driver security validation requirements make them slow on desktop.
> 
> Start with texture arrays. How many different sizes do you really need? 2<sup>8,9,10,11,12</sup> x 3 formats = 18 arrays. Make a config param for each array, statically allocate them at load time and overwrite them repeatedly as needed.
> 
> - Compress your textures with [https://github.com/richgel999/bc7enc\_rdo](https://github.com/richgel999/bc7enc_rdo) then with [https://github.com/facebook/zstd](https://github.com/facebook/zstd)
> - Make a 64 MB "Persistent Mapped Buffer" once at init. [https://www.cppstories.com/2015/01/persistent-mapped-buffers-in-opengl/](https://www.cppstories.com/2015/01/persistent-mapped-buffers-in-opengl/) That's enough to handle 16 4k textures in flight.
> - Memory-map your zSTD compressed file and decompress it into your persistent mapped buffer. You can do this from any thread because it doesn't actually involve any OpenGL calls.
> - glBindBuffer(GL\_PIXEL\_UNPACK\_BUFFER, yourPMBuffer)
> - glCompressedTexSubImage3D() with target=GL\_TEXTURE\_2D\_ARRAY, specifying the layer with the zoffset parameter
> - `GLsync fence = glFenceSync(GL_SYNC_GPU_COMMANDS_COMPLETE, 0);` so you can find out when the TexSubImage is done and you can reuse that part of the buffer.
> 
> > **sansisalvo3434** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm61p6s/) •
> > 
> > I suppose I'll need to manage 18 different array types with offsets. I use the material index to access materials/textures in the GPU. (I use indirect rendering)  
> > Should I store the material and texture separately or together? (for your scenario.)
> > 
> > Another question is:
> > 
> > How can I determine the appropriate format for saving? (i read the article your first suggestion and i understood)
> > 
> > Thanks for help.
> > 
> > > **corysama** • [2 points](https://reddit.com/r/GraphicsProgramming/comments/1ojfw3p/comment/nm8qmyj/) •
> > > 
> > > Here's how I'd do it
> > > 
> > > - A model is a mesh and a list of material instances.
> > > - A mesh is a chunk of triangles loaded as a unit, but the triangles are sorted into ranges (called "submeshes") where each contiguous range uses the corresponding material in the model's material list. So, at a high level you want to draw a mesh, but that gets broken down into drawing 1 submesh for the skin, 1 for the clothes and 1 for the hair because they use different materials.
> > > - A material is the prototype for a material instance. It contains all the params that don't change per instance and the defaults for params that do. That includes numeric parameters and references to textures.
> > > - A material instance is a copy of the prototype with the specific values for a specific instance.
> > > - A texture asset has a reference to the texture array and the index into that array
> > > 
> > > There are lots of references to each other between these assets. They should probably be packed together into the same file, assuming you are using some sort of pak file container. But, pack them together with lots of other assets so multiple meshes can reference the same material and multiple materials can reference the same textures.
> > > 
> > > In your art pipeline, it's best to not have the artists label textures as specific BCn formats unless they really have to. Better to have them say "This is an Albedo texture. This is a Normal Map. This is a Height Map." and have the art pipeline decide which format to use. Having a source asset specify "This should be BC1" should be for special-cases. That gives your art pipeline and runtime a lot of flexibility to optimize and makes life simpler for artists.
> > > 
> > > Forget my original texture format advice. I'm out of practice. [https://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/#comparison-table](https://www.reedbeta.com/blog/understanding-bcn-texture-compression-formats/#comparison-table) has a pretty good breakdown of good uses of different formats.
> > > 
> > > - BC7 for albedo, specular, general RGBA, or packing correlated monochrome images together
> > > - BC6 for HDR skyboxes
> > > - BC5 for normal maps
> > > - BC4 for monochrome height/roughness/etc maps
> > > - Don't worry about BC3&2
> > > - BC1 for cheap RGB and optional 1-bit alpha. Ex: detail textures, leaves, hard-edged particle sprites
> > > 
> > > You could probably break out BC6 as special case that doesn't bother to use texture arrays. So, you end up with 4 formats x 5 sizes = 20 arrays for the bulk of your draws.
> > > 
> > > Once you get this set up, it can technically work. Most of your assets should be set up to use fixed size ratios between their textures. Like `albedo,specular = 1x, roughness,metalness = 0.5x, normal = 2x, detail at a fixed size`. But, that's still a pain and inflexible.
> > > 
> > > So, then you can move on to bindless. Instead of 1000s of textures, you'll just have 20 texture arrays. But, you can freely mix and match them per draw instead of having fixed recipes.
> > > 
> > > A thing to be aware of though even with bindless, when you use instancing all of the instances in a draw will need to use the same texture array. When you do a multidraw with instances, the separate draws in the multidraw can pick different bindless texture arrays for each of their albedos, but instances of the same draw can only use different indexes into the same array.
> > > 
> > > Very new hardware doesn't have this restriction. Mid-range hardware can work around it with slower shaders. But, it's best to deal with the restriction for now. In OpenGL they refer to this as "Dynamically Uniform". Basically, instances can get packed into the same "subgroup/wave/warp" in the GPU. And, all of the threads in that group need to access the same sampler at the same time. Draws in a multidraw don't get packed like that. That makes them slower in general, but they can switch samplers between draws.