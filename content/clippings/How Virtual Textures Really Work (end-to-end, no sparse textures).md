---
title: "How Virtual Textures Really Work (end-to-end, no sparse textures)"
source: "https://www.reddit.com/r/GraphicsProgramming/comments/1qvoqbn/how_virtual_textures_really_work_endtoend_no/"
author:
  - "[[shlomnissan]]"
published: 2026-02-04
created: 2026-02-05
description: "Reddit is where millions of people gather for conversations about the things they care about, in over 100,000 subreddit communities."
tags:
  - "clippings"
---
I just published a deep dive on virtual texturing that tries to explain the system end-to-end.

The article covers:

- Why virtual texturing exists (screen space, not “bigger textures”)
- How mip hierarchies + fixed-size pages actually interact
- GPU addressing vs CPU residency decisions
- Feedback passes and page requests
- What changes once you move from 2D to 3D sampling
- A minimal prototype that works without hardware sparse textures

I tried to keep it concrete and mechanical, with diagrams and shader-level reasoning rather than API walkthroughs.

Article: [https://www.shlom.dev/articles/how-virtual-textures-work](https://www.shlom.dev/articles/how-virtual-textures-work)

Prototype code: [https://github.com/shlomnissan/virtual-textures](https://github.com/shlomnissan/virtual-textures)

Would love feedback from people who’ve built VT / MegaTexture-style systems, or from anyone who’s interested.

---

## Comments

> **nickludlam** • [8 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3j1yee/) •
> 
> Your article link is a 404. It should be [https://www.shlom.dev/articles/how-virtual-textures-work/](https://www.shlom.dev/articles/how-virtual-textures-work/)

> **corysama** • [6 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jbtbb/) •
> 
> Your description says “Why virtual texturing exists (screen space, not “bigger textures”)”. Maybe I read the article too fast. But, I see a lot of discussion of Big Textures and nothing in particular about screen space motivations.
> 
> Fun fact: Baldur’s Gate Dark Alliance for the PS2 & GameCube used a “unique texturing” scheme similar to megatextures but with automation instead of virtualization. The artists used the standard materials and lighting features of Autodesk 3D Studio and the art pipeline baked out a single layer of unique textures for every surface in the level static geometry. The in-game camera pivoted around the z axis at a high fixed angle enabling the run time to stream textures in on the fly as you moved through the level.
> 
> > **shlomnissan** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jfci8/) •
> > 
> > That’s fair! The screen-space motivation is there, but maybe it needs to be called out more:
> > 
> > "*The limiting factor when rendering large textures is not memory or bandwidth, but screen resolution. Because a screen has a fixed number of pixels, only the portion of a texture that projects onto the screen can contribute to the final image.*
> > 
> > *Suppose you have a 24k texture projected onto a 4k display. The texture is six times larger so it can never be seen at full resolution all at once. Zoomed out the screen downsamples it and only a fraction of the pixels contribute to the image. Zoomed in more detail becomes visible but only over a small region at a time.*"
> > 
> > \>  The in-game camera pivoted around the z axis at a high fixed angle enabling the run time to stream textures in on the fly as you moved through the level.
> > 
> > That's really interesting!!

> **mister\_cow\_** • [3 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3j1vpa/) •
> 
> I'm getting a 404

> **shlomnissan** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3j4ly1/) •
> 
> Thanks
> 
> > **corysama** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3j9i6q/) •
> > 
> > The markdown for the links is still mixed up. The syntax is
> > 
> > `[description](url)`
> > 
> > Or, you can just put the URL directly without any adornment.
> > 
> > > **shlomnissan** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jfldu/) •
> > > 
> > > Thanks! I updated it. I copied these links from a markdown document :/

> **fllr** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jepgc/) •
> 
> I liked the read :) thanks!
> 
> > **shlomnissan** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jfms8/) •
> > 
> > Thanks :)

> **cybereality** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3jolyr/) •
> 
> very nice. gonna read this later, but i skimmed it and looks cool.

> **Plazmatic** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3k44d0/) •
> 
> Why are texture atlasses used instead of just arrays of textures where you can just actually define where memory is going to be stored in an allocation and not deal with any of the edge cases found in texture atlasses? Or are you just demonstrating what was used before modern graphics APIs?
> 
> > **noradninja** • [1 points](https://reddit.com/r/GraphicsProgramming/comments/1qvoqbn/comment/o3k7e6r/) •
> > 
> > I mean, this is useful for me because I am deploying to the Vita and it doesn’t support texture arrays. I may give this a whirl. Thanks, OP.