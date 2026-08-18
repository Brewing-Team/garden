---
title: "h3r2tic's grimoire"
source: "https://h3.gd/"
author:
published:
created: 2025-11-01
description: "Technobabble and nonsense"
tags:
  - "clippings"
---
[![](https://h3.gd/processed_images/banner.0a1fb42ff7f81955.jpg)](https://h3.gd/kajiya/)

💡 Experimental real-time global illumination... toy 🦀

Done in my spare time at Embark, `kajiya` is an evolving excursion into real-time global illumination algorithms. Having gone through surfels and morphological inverse cone tracing (🤪), it's now fully infused with ReSTIR and irradiance caching.

Permissively licensed [on GitHub](https://github.com/EmbarkStudios/kajiya/).

[![](https://h3.gd/processed_images/banner.15fb2c5386c67200.png)](https://h3.gd/unholy-fusion-rust-physx/)

Unsafe automatically-generated Rust bindings for the NVIDIA PhysX C++ API.

[![](https://h3.gd/processed_images/banner.4adb25096896a9e5.png)](https://h3.gd/raytracing-in-hybrid-real-time-rendering/)

At SEED we developed a mini-game for autonomous agents: PICA PICA. It was the cutest Skynet implementation around.

It used a hybrid renderer: rasterization meets raytracing meets specialized denoising. I worked on global illumination, reflections, shadows, and a bunch more.

[![](https://h3.gd/processed_images/runobj2.3766d3dffa8f666c.png)](https://h3.gd/how-not-to-use-dlls/)

Runtime loading of object files, relocation of DLLs. Mostly harmful stuff.

[![](https://h3.gd/processed_images/banner.febc2ea87c6807f4.png)](https://h3.gd/a-deferred-material-rendering-system/)

Practical application of the GCN hacks: indirect dispatch of lots of unique compute shaders and native barycentric coordinate access. Those allows for efficient surface shading in a deferred manner without the use of ubershaders. Geometry and material descriptions can be decoupled, and we gain a lot of control over shading frequency. [Slides here!](https://onedrive.live.com/view.aspx?resid=EBE7DEDA70D06DA0!115&app=PowerPoint&authkey=!AP-pDh4IMUug6vs)

[![](https://h3.gd/processed_images/banner.26d1e944c6a4276f.png)](https://h3.gd/hacking-gcn-via-opengl/)

AMD’s Graphics Core Next GPU architecture has a number of interesting features which one cannot access via standard APIs. I show how to hack around the OpenGL driver, and feed it native shaders written in GCN ISA instead of GLSL. [Slides here!](https://onedrive.live.com/view.aspx?resid=EBE7DEDA70D06DA0!107&app=PowerPoint&authkey=!AD-O3oq3Ung7pzk)

<iframe xmlns="http://www.w3.org/1999/xhtml" src="https://player.vimeo.com/video/115108688?autoplay=1&amp;loop=1&amp;title=0&amp;byline=0&amp;portrait=0" height="256" frameborder="0"></iframe>

Importance sampled screen-space reflections with a novel spatiotemporal filter. I prototyped it in a toy engine written in the Rust language, and later ported to Frostbite, working closely with Yasin Uludag. It first shipped in Mirror’s Edge and Need for Speed.

Check out the slides for my Siggraph 2015 talk which was part of [Advances in Real-Time Rendering in Games](http://advances.realtimerendering.com/s2015/).