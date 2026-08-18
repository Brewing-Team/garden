---
title: Voxel Displacement Renderer — Where This Goes From Here
source: https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/
author:
published: 2024-05-19
created: 2025-09-27
description: Screenshots of the renderer over time, from very early in development to today. This is the second of two posts about a renderer I have been developing, focusing on why I've built it and my plans for the future. The first post discusses what I've built and how it works. In the first post, I described what I've been building — a custom renderer that uses voxels and displacement mapping to modernize the look of classic 3D games. Here, I want to talk about why I started working on this, why I've continued to develop it, and the prospect of working with people and using this rendering technique in a game. [...]
tags:
  - clippings
  - voxel
---
![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/cover_why_01_1280.jpg)

Screenshots of the renderer over time, from very early in development to today.

*This is the second of two posts about a renderer I have been developing, focusing on why I've built it and my plans for the future. The [first post](https://blog.danielschroeder.me/blog/voxel-displacement-modernizing-retro-3d/) discusses what I've built and how it works.*

In the first post, I described what I've been building — a custom renderer that uses voxels and displacement mapping to modernize the look of classic 3D games. Here, I want to talk about why I started working on this, why I've continued to develop it, and the prospect of working with people and using this rendering technique in a game.

## Why I started working on this

To explain why I started working on this project, it helps to go over a bit of my background. I became interested in computer graphics in college, working on side projects to learn more. After college, I entered a PhD program to continue exploring the subject. While I learned a lot there, I also discovered that academia didn't align well with my motivations; I like *building* things, not just proving that they can be built. So I left grad school and took a job at Google. While there, I worked on general backend software engineering problems, not graphics. Taking a hobby or interest and turning it into your job, like I did in grad school, carries risks, and I felt like I needed a break from that.

Fast forward to during the pandemic. Like many people, I started thinking about whether I wanted to make a change — in my case, returning to working in graphics. I had a lot of relevant knowledge and skill, but my last work experience in that space was in 2014, and technologies change.

So, I decided to take some time and work on a self-directed project in real-time graphics — to dust off my skills, learn about new technologies, and build something I could show to employers to demonstrate my abilities. The problem I ultimately decided to experiment with was the voxel displacement mapping idea described in the previous post. I wrote down some ideas, made a new repository, and started building...

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/early_grass_hill_01.jpg)

Every project starts somewhere. In this case, "somewhere" meant "radioactive-green grassy hills."

## Why I've continued building this

When I started working on this project, I had no idea what it would become. In graphics, it's easy to pick an interesting problem, come up with a cool idea for how to solve it, build what you've designed — and discover that it runs at 10 frames per second. It was a pleasant surprise, then, when my early experiments ran quite well (it turns out that GPUs are faster than they used to be — who knew).

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/early_prototype_and_mesh_02_b.jpg)

Screenshots from further into development. At first I could only apply voxel displacement to a few hard-coded shapes like cubes (left). Generalizing the technique to work on triangle meshes (right) was very hard. This was still before I had implemented lighting.

Seeing how well this was working, I decided to give the project some more time. In particular, I wanted to see whether I could build the complicated machinery that would allow me to apply voxel displacement textures to a wide range of triangle-mesh geometry. As I continued to work on this problem — adding features, improving performance, implementing lighting — I realized that it might actually be viable to use this rendering technique in a game, which I very much did not expect at the start.

As such, I decided to take this further and flesh out a proper demo of my renderer. I kept my work relatively private; before I shared this with a wider audience, I wanted to convince *myself* that it would be possible to use this rendering technique in a game — in terms of performance, visual quality, and flexibility of the content creation process. I've now reached that point. To be clear, there's still more work to do; but I now trust that it's doable.

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/early_testing_stone_block_01.jpg)

Testing the new materials for the demo environment. Adding lighting to the renderer had a huge impact on the visuals.

## Portfolio piece, or something more

Moving forward, I'm considering two rough paths for where to go with this. The safe route is to follow the original plan: use this project as a portfolio piece and get a job doing graphics programming, whether in games or not. That would be fine, at the end of the day.

But darn it, this project is really cool, and nothing else I've seen is quite like it. Game developers and players who've tried this demo in person have been enthusiastic about it — whether they have nostalgia for the era of games that inspired the aesthetic, or are seeing it with fresh eyes. I'm reasonably happy with the assets I've made for the demo, but I would love to see what real artists could do with this. And these assets — low-poly triangle meshes and textures — are the sort of thing that a *small* team can produce.

With all that in mind, I'm exploring whether there's a good path forward to work with people and use what I've been building in a game. The question is what such a path could look like, and how to get there.

## How this becomes part of a game

"Working with people and using this in a game" is a... vague phrase. What would it take to make that happen? Who am I interested in working with, and how? What would it look like to use this rendering tech in a game? And what more machinery needs building before that can happen?

In the rest of this post, I'll explore these questions. I want to be clear: I don't have all the answers at this point. **I'm still thinking about this and exploring my options.** A big part of why I'm writing these posts now is to share my story with more people, get this work in front of more eyeballs, and reach folks who may have ideas — or who may be interested in working with me down the line. So if you're curious, let's dive in.

## Putting this in an engine

For now, what I've built is a renderer, and an interactive demo to show it off. To develop a game with this visual style, you'd need the broader features of a game engine. As I described in more detail in the first post, because the environment geometry is created as triangle meshes and the voxels are just surface detailing, I think it makes more sense to integrate this rendering technique into an existing engine than to build my own.

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/mesh_before_after_02.jpg)

A more extreme example of displacement, used here to form the stairs of the spiral staircase. In the input mesh (left), the staircase is just a ramp. In my demo (right), the mesh is still used for collision, so player movement up and down the staircase is smooth.

All the major engines provide the ability to customize rendering at a lower level. While my workload is unusual, its use of the underlying graphics API is relatively basic, so the lower-level rendering abstractions provided by the engines should be sufficient to implement it. Performing this engine integration wouldn't be simple, but it's certainly doable <sup><a href="https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/#fn-engine-integration">1</a></sup>.

A notable challenge here is deciding which engine to use, and when to move this into an engine instead of continuing to develop more features in the standalone codebase. For now, I plan to make further improvements in the existing codebase as I consider my options <sup><a href="https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/#fn-godot">2</a></sup>.

## Impact on development process

Say I've migrated the current features of the renderer into game engine X. Using this visual style instead of the engine's default renderer would primarily affect art asset creation and level design; other aspects of development, like game logic, scripting, player and enemy movement physics, AI, UI/UX, etc., should look pretty normal.

The way I see it, the most interesting question would be what tools and workflow to use to create the environment geometry. As one example, it *wouldn't* work to do what some recent retro-inspired first person shooters have done and use a Quake level editor, because the renderer needs shading normals for the meshes to identify smooth regions and guide the behavior of the displacement. For my demo, I've used Blender both to make the models and to assemble the overall scene. Honestly, I'd need to do more research into what kinds of workflows other developers have used for authoring low-poly environments for modern games.

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/blender_demo_03.jpg)

A section of the demo environment in Blender.

Moving to the textures, I don't think there's much to say here; it should be possible to create the albedo and displacement using any software of choice. I do have some ideas for tools I could build to speed up texture creation, particularly for managing variants of a given texture, but that's a longer story.

## Remaining features to build

So far I've talked about how to integrate the *existing* functionality of my renderer into a game engine and use it during development. There are more features I'd need to build to make this usable in a game, however, which I'd likely prototype before moving the renderer into an engine.

Most important is adding support for animated elements like enemies, as well as smaller objects (e.g., lanterns on the wall, pots on the floor). The voxel displacement machinery I've built is great for creating large, detailed environments, but it isn't well suited to modeling smaller or thinner features, and is intended for static meshes only <sup><a href="https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/#fn-animating-meshes">3</a></sup>.

How would you handle enemies or small objects, then? This is both a technical question and an aesthetic one, and there's no single correct answer. You have to balance rendering performance, art style, ease of asset creation, and cohesion with the existing visuals. I'll talk about my preferred idea in a future post, but for right now, the point is that this is something I would still have to build before you could create a full gameplay experience in this visual style.

Another area for improvement is lighting. I haven't talked about the lighting much yet, because it's deceptively simple. While there's some complexity in how I shade the voxels, the lighting in the demo environment is just a set of non-shadow-casting point sources and an ambient light. For the graphics folks, I don't even cull them yet; every fragment evaluates every light source in a forward pass.

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/lighting_components_03_1k_c.jpg)

Visualizations of albedo (top left), normals (top right), lighting (bottom left), and the finished image (bottom right) for a section of the scene. The lighting makes it much easier to see the uneven heights of the stone blocks.

Scaling this up to handle many lights won't be an issue — there are various ways to tackle that problem. More interesting is supporting shadows or higher-order lighting effects like global illumination. Again, this is as much an art-style question as a technical one; the games that inspired these visuals have relatively simple lighting, after all, and even the current implementation looks surprisingly good. For dynamic direct shadows, I have some promising ideas. Beyond that, baking is a possibility, though it may or may not be appropriate depending on the gameplay and the desired visual style.

## Making this available to others

Finally, let's talk about the people side of developing a game with this visual style. What opportunities am I interested in exploring? To illustrate my thinking, I'll start with one path I *won't* be taking: some folks I've shown this demo to have asked whether I would consider releasing this as an asset for an engine asset store, or more generally as a widely available middleware. Ultimately, I think that would be a terrible idea.

While I'm aiming for it to be fast and relatively easy to create art assets for this visual style, there *is* a learning curve, and the meshes in particular have to be authored with this use case in mind. This isn't a magic "make things look awesome" filter that you can slap onto a project at any stage of development.

Another factor is that when you take a tool, pack it in a pretty box, and put it out there for anyone to use, you need to meet the requirements of a large class of hypothetical future users with different needs, skills, and goals. By comparison, if I work with a single team on a single project, I can focus on meeting the concrete needs of that team and that project, shaping the tech and the tools accordingly. As an analogy, this is why it remains possible for some studios to develop in-house engines that compete on graphical fidelity with big-budget Unreal Engine titles.

Finally, the way I see it, one of the big reasons to use this in a game would be to help differentiate it, to create something that feels fresh and compelling. It's notoriously hard for games to stand out from the crowd these days. If I put this out there for any developer to use as they wished, that would dilute its potential impact.

![](https://blog.danielschroeder.me/blog/voxel-displacement-where-this-goes/loft_overview.jpg)

## Who to work with, and how

So one way or another, I believe that the only realistic path for this to become part of a game is for me to work on an ongoing basis with other developers to get a project across the finish line. But what developers, and what working arrangement?

I've had some folks suggest to me that I start my own team and lead a project. I'm not *categorically* opposed to that path. That said, the simple fact is that my professional experience isn't in game development (or in management). There are valuable experiences, hard-earned lessons, etc. in that space that I have not had the opportunity to gain. For my part, the point of taking this further wouldn't be to puff up my ego; it would be to build something successful, leveraging the experience that I *do* bring.

With all that said, there are two routes that seem most plausible to me at this point. One would be to partner with an existing studio or team that wants to pursue the "modernized retro 3D" visual style this renderer makes possible. If that's you, and you're intrigued by what you're seeing and want to learn more,**then please get in touch!** (My email is at the bottom of the page.) As I've described, this work isn't ready to use just yet — and it isn't set in stone either, including the decision of which game engine to use. So don't worry if your timeframe is longer.

The other route would be for me to partner with one or a small number of developers with complementary skills and experience to start something new that can be stronger than the sum of its parts. The obvious challenge for that route would be to find the right people and build up a relationship with them. If you're a game developer with your own skills and experience to bring to the table, and you look at this and think "imagine what *I* could build with that," **then go ahead and tell me about yourself!**

Of course, there's no guarantee that there will be a good path to use this work for anything more than its original purpose: as a portfolio piece. You can reach your own conclusions about how likely it is that this becomes something more. What I do know already is that working on this project has been incredibly educational, and a valuable experience for me personally. If it can become something more, then great!

In any case, I'll continue working on new features and other improvements in the coming months as I think about my options and talk to more people. I can't say how often I'll update this blog or the YouTube channel — even writing these two posts took longer than I'd care to admit — though I'm sure there will be more to come. If you made it to the end of this post as well, then thank you for reading!