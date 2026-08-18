---
title: "ntsc-rs - an accurate VHS video effect"
source: "https://ntsc.rs/"
author:
published:
created: 2026-07-05
description: "ntsc-rs is a free, open-source VHS and analog TV video effect. Use it online in your browser, as a standalone application, or as a plugin for DaVinci Resolve, After Effects, and more."
tags:
  - "clippings"
---
![Screenshot of the ntsc-rs application](https://ntsc.rs/assets/images/dMI5kPlcVt-1204.webp)

ntsc-rs is a free, open-source video effect which accurately emulates analog TV and VHS artifacts.

![Side-by-side comparison between Red Giant Universe VHS and ntsc-rs](https://ntsc.rs/assets/images/rclvL530NQ-720.webp)

Other popular effects eyeball the look of VHS tapes using simple color lookup tables and overlays. ntsc-rs uses algorithms that model how NTSC transmission and VHS encoding actually work, based on algorithms developed in [composite-video-simulator](https://github.com/joncampbell123/composite-video-simulator/), [zhuker/ntsc](https://github.com/zhuker/ntsc), and [ntscQT](https://github.com/JargeZ/ntscqt/).

![An ntsc-rs render which has completed in 15 seconds overlaid atop lines of code](https://ntsc.rs/assets/images/sBL4MSmwhO-813.webp)

ntsc-rs is written in Rust, and is multithreaded and SIMD-accelerated. Unlike similar effects such as ntscQT, it can run in real time at much higher resolutions than actual NTSC footage.

![ntsc-rs running as a plugin in nonlinear editing software](https://ntsc.rs/assets/images/j3LH5hwZRj-1445.webp)

ntsc-rs is available not just as a standalone and web application, but also as a plugin for After Effects, Premiere, and all OpenFX-compatible software. This includes DaVinci Resolve, Hitfilm, and Vegas.

[Download ntsc-rs version 0.9.4](https://ntsc.rs/download) [Try it online](https://web.ntsc.rs/)