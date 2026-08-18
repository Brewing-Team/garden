---
title: "Implementing a tiny CPU rasterizer"
source: "https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer.html"
author:
  - "[[lisyarus blog]]"
published:
created: 2025-05-31
description:
tags:
  - "clippings"
---
Implementing a tiny CPU rasterizer

  

2024 Oct 30

  

This is a tutorial series on implementing a basic CPU rasterization engine in C++ from scratch. No GPU involved, just drawing pixels with our bare hands, emulating what the GPU usually does for us.

The tutorial is split into 12 parts, each covering some aspect of the engine, from drawing our first pixels to advanced stuff and optimizations. ***Some parts of the tutorial are not finished yet, this is a work-in-progress.***

All the code for this project is available [on GitHub](https://github.com/lisyarus/tiny-rasterizer), with a single commit corresponding to each article in the series.

- [Part 1: Clearing the screen](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-1.html)
- [Part 2: Drawing a triangle](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-2.html)
- [Part 3: Interpolating colors](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-3.html)
- [Part 4: Changing perspective](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-4.html)
- [Part 5: Fixing issues with 3D](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-5.html)
- [Part 6: Adding some depth](https://lisyarus.github.io/blog/posts/implementing-a-tiny-cpu-rasterizer-part-6.html)
- Part 7: Shedding some light *(work in progress)*
- Part 8: Texturing *(work in progress)*
- Part 9: Loading models *(work in progress)*
- Part 10: Rendering to texture *(work in progress)*
- Part 11: Shadow mapping *(work in progress)*
- Part 12: Optimization *(work in progress)*

---

Hey, if you like my articles, consider supporting my other work!

For example, watch my [YouTube devlogs](https://youtube.com/@lisyarus), like this one:

![](https://www.youtube.com/watch?v=nAfVL_OD5G8)

---