---
title: Radeon™ Rays - AMD GPUOpen
source: https://gpuopen.com/radeon-rays/
author:
published:
created: 2025-09-21
description: The lightweight accelerated ray intersection library for DirectX®12 and Vulkan®.
tags:
  - clippings
  - ray-tracing
---
Radeon Rays

Radeon™ Rays is our high-efficiency, high-performance ray intersection acceleration library as seen in [Radeon™ ProRender](https://gpuopen.com/radeon-pro-render/).

It supports a range of use cases, including interactive light baking for game development workflows, and real-time indirect sound simulation.

Supports:

- DirectX®12.
- Vulkan®.

This release adds the following:

- Open Source.
- Logging mechanism for easier debugging.
- Set of tests to validate changes to the source code.

### Which version should I use?

AMD has developed Radeon™ Rays for many years. If you require OpenCL™ support, please use [Radeon™ Rays 2.0](https://github.com/GPUOpen-LibrariesAndSDKs/RadeonRays_SDK/tree/legacy-2.0).

## Features

### Custom AABB

Guide the construction of the Bounding Volume Hierarch (BVH) by providing a custom AABB hierarchy for your scene.

### GPU BVH Optimization

Optimizes the Bounding Volume Hierarchy (BVH) specifically for efficient GPU access.

Find [Radeon™ Rays source](https://github.com/GPUOpen-LibrariesAndSDKs/RadeonRays_SDK) on GitHub.

AMD developed Radeon™ Rays to help developers get the most out of AMD GPUs, as well as save them from maintaining hardware-dependent code. Radeon™ Rays exposes a well-defined C API for scene construction and performing asynchronous ray intersection queries. It is not limited to AMD hardware or a specific operating system.

Radeon™ Rays can be easily distributed, and through its API helps assure compatibility and best performance across a wide range of hardware platforms.

**Additional features:**

- Supports DirectX®12 and Vulkan®.
- Geometry update without full rebuild.
- Logging mechanism for easier debugging.
- Set of tests to validate changes to the source code.

![AMD Radeon Rays](https://gpuopen.com/_astro/rays1.7nmY6Cg__zT3f9.jpg)

## Requirements

CMake 3.12 and above.

spdlog library installed for logging.

- **DirectX®12**: a 64-bit version of Windows® 10, and a GPU and drivers that support DirectX®12 features including Shader Model 6.0.
- **Vulkan®**: a 64-bit version of Windows® 10 or Linux, and a GPU and drivers that support Vulkan® version 1.2.

Microsoft® Visual Studio 2013 or later must be installed to compile the sample renderer.

## Version history

### Related software

[![Radeon™ ProRender Suite](https://gpuopen.com/_astro/featured-20457311-C_AMD_Radeon_ProRender_Developer_Suite_Lockup_RGB_Wht.DvdwCfzm_Z1bpwBA.jpg)](https://gpuopen.com/radeon-prorender-suite/)

[Radeon™ ProRender Suite](https://gpuopen.com/radeon-prorender-suite/)

[

AMD Radeon™ ProRender is our fast, easy, and incredible physically-based rendering engine built on industry standards that enables accelerated rendering on virtually any GPU, any CPU, and any OS in over a dozen leading digital content creation and CAD applications.

](https://gpuopen.com/radeon-prorender-suite/)

[![AMD Radeon™ ProRender SDK](https://gpuopen.com/_astro/featured-18147992-E_AMD_Radeon_ProRender_Lockup_RGB_Wht.UWChwYsM_ZKzkwN.jpg)](https://gpuopen.com/radeon-pro-render/)

[AMD Radeon™ ProRender SDK](https://gpuopen.com/radeon-pro-render/)

[

AMD Radeon™ ProRender SDK is a powerful physically-based path traced rendering engine that enables creative professionals to produce stunningly photorealistic images.

](https://gpuopen.com/radeon-pro-render/)

[![Orochi](https://gpuopen.com/_astro/featured-231825264-A_AMD_Orochi_Lockup_RGB_Wht.YcgioIhl_ZoHq0d.jpg)](https://gpuopen.com/orochi/)

[Orochi](https://gpuopen.com/orochi/)

[

Orochi is a library which loads HIP and CUDA® APIs dynamically, allowing the user to switch APIs at runtime.

](https://gpuopen.com/orochi/)

[![AMD FidelityFX™ Hybrid Shadows sample](https://gpuopen.com/_astro/FFX_HybridShadows_DebugRays.B9j3_0LC_Z1OzKO7.jpg)](https://gpuopen.com/fidelityfx-hybrid-shadows/)

[AMD FidelityFX™ Hybrid Shadows sample](https://gpuopen.com/fidelityfx-hybrid-shadows/)

[

This sample demonstrates how to combine ray traced shadows and rasterized shadow maps together to achieve high quality and performance.

](https://gpuopen.com/fidelityfx-hybrid-shadows/)

### Related news and technical articles

[![Enhancing AMD Radeon GPU Detective Output with DirectX Debug Information](https://gpuopen.com/_astro/RGD_shader_debug_info_1.GZwEhCeI_Z25GD0j.jpg)](https://gpuopen.com/learn/enhancing-amd-radeon-gpu-detective-output-with-directx-debug-information/)

[Enhancing AMD Radeon GPU Detective Output with DirectX Debug Information](https://gpuopen.com/learn/enhancing-amd-radeon-gpu-detective-output-with-directx-debug-information/)

[

With version 1.5 of AMD Radeon™ GPU Detective (RGD) you can now use the debug information that is produced by the Microsoft DirectX® Shader Compiler.

](https://gpuopen.com/learn/enhancing-amd-radeon-gpu-detective-output-with-directx-debug-information/)

[![Using Neural Networks for Geometric Representation](https://gpuopen.com/_astro/LSNif_article_title.CYwMXfEw_QmTE.jpg)](https://gpuopen.com/learn/using_neural_networks_for_geometric_representation/)

[Using Neural Networks for Geometric Representation](https://gpuopen.com/learn/using_neural_networks_for_geometric_representation/)

[

Explore how Neural Intersection Functions (NIF) and the enhanced LSNIF are poised to reshape ray tracing by replacing traditional BVH traversal with efficient, GPU-friendly neural networks for accelerated performance and high-fidelity imagery.

](https://gpuopen.com/learn/using_neural_networks_for_geometric_representation/)

[![CPU performance optimization guide - part 4](https://gpuopen.com/_astro/featured-programming-red.C-bD--wM_vWDkh.jpg)](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part4/)

[CPU performance optimization guide - part 4](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part4/)

[

Optimize CPU performance by manually writing x64 assembly code, offering a detailed comparison with compiler-generated instructions and achieving improved performance through streamlined instruction sets.

](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part4/)

[![CPU performance optimization guide - part 3](https://gpuopen.com/_astro/featured-programming-red.C-bD--wM_vWDkh.jpg)](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part3/)

[CPU performance optimization guide - part 3](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part3/)

[

We look at optimizing CPU performance by reducing the number of instructions, and highlights methods to enhance instruction efficiency and algorithm throughput.

](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part3/)

[![CPU performance optimization guide - part 2](https://gpuopen.com/_astro/featured-programming-red.C-bD--wM_vWDkh.jpg)](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part2/)

[CPU performance optimization guide - part 2](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part2/)

[

Part 2 of the CPU performance optimization guide explores cache invalidation issues, benchmarking, and prefetch optimization strategies for improved memory performance.

](https://gpuopen.com/learn/cpu-performance-guide/cpu-performance-guide-part2/)

[![Work Graph Playground a learning framework for GPU Work Graphs](https://gpuopen.com/_astro/workgraph-playground.BwuqwLi0_2bqfcl.jpg)](https://gpuopen.com/learn/work-graph-playground/)

[Work Graph Playground a learning framework for GPU Work Graphs](https://gpuopen.com/learn/work-graph-playground/)

[

Read about our latest sample for D3D12 GPU Work Graphs. We're making Work Graphs more accessible with a tutorial framework.

](https://gpuopen.com/learn/work-graph-playground/)

[![Meshlet compression](https://gpuopen.com/_astro/mesh-shader-pipeline.DSbHUTmv_Z2qh0ML.jpg)](https://gpuopen.com/learn/mesh_shaders/mesh_shaders-meshlet_compression/)

[Meshlet compression](https://gpuopen.com/learn/mesh_shaders/mesh_shaders-meshlet_compression/)

[

We show how to diminish the memory footprint of meshlet geometry, thus both the index buffer and the vertex attributes. Decompression then happens on the fly on every frame in the mesh shader.

](https://gpuopen.com/learn/mesh_shaders/mesh_shaders-meshlet_compression/)

[![Microsoft® DirectSR has integrated AMD FidelityFX™ Super Resolution 3.1](https://gpuopen.com/_astro/AMD_FSR3_1_blog_top_banner.DSM5W9r3_Zjwcff.jpg)](https://gpuopen.com/learn/microsoft_directsr_now_supports_amd_fidelityfx_super_resolution_3-1/)

[Microsoft® DirectSR has integrated AMD FidelityFX™ Super Resolution 3.1](https://gpuopen.com/learn/microsoft_directsr_now_supports_amd_fidelityfx_super_resolution_3-1/)

[

This integration enhances upscaling capabilities, offering improved temporal stability and detail preservation.

](https://gpuopen.com/learn/microsoft_directsr_now_supports_amd_fidelityfx_super_resolution_3-1/)

### Related videos

[![GPU Reshape – Modern Shader Instrumentation and Instruction Level Validation (Digital Dragons 2024) – YouTube link](https://gpuopen.com/_astro/gpureshape-dd-image.CSlUOVJp_1TxTlp.jpg)](https://gpuopen.com/videos/gpu-reshape-digital-dragons-2024/)

[GPU Reshape – Modern Shader Instrumentation and Instruction Level Validation (Digital Dragons 2024) – YouTube link](https://gpuopen.com/videos/gpu-reshape-digital-dragons-2024/)

[

GPU Reshape is, a just-in-time instrumentation framework with instruction level validation of shaders. A deep dive into current validation methodologies, and what the future of instrumentation may hold.

](https://gpuopen.com/videos/gpu-reshape-digital-dragons-2024/)

[![Mesh Shaders – Learning Through Examples (Digital Dragons 2024) – YouTube link](https://gpuopen.com/_astro/meshshaders-examples-thumbnail.CkuOHE-J_9T6rq.jpg)](https://gpuopen.com/videos/mesh-shaders-learning-examples/)

[Mesh Shaders – Learning Through Examples (Digital Dragons 2024) – YouTube link](https://gpuopen.com/videos/mesh-shaders-learning-examples/)

[

Learn about the new Mesh Shader pipeline which can help to create even more better-looking games.

](https://gpuopen.com/videos/mesh-shaders-learning-examples/)

[![DirectStorage: Optimizing Load-time and Streaming (GDC 2023 - YouTube link)](https://gpuopen.com/_astro/DirectStorage-Thumbnail-featured.CUwm-hBx_ZhUnvz.jpg)](https://gpuopen.com/videos/gdc-2023-directstorage/)

[DirectStorage: Optimizing Load-time and Streaming (GDC 2023 - YouTube link)](https://gpuopen.com/videos/gdc-2023-directstorage/)

[

Join us for a presentation about DirectStorage and how to integrate it to extract optimal load time and streaming performance.

](https://gpuopen.com/videos/gdc-2023-directstorage/)

[![Memory Management in the APEX Engine - Digital Dragons 2022](https://gpuopen.com/_astro/MemoryManagementInAPEX_v2_featured.CEanE--j_Zui9a3.png)](https://gpuopen.com/videos/memory-management-in-the-apex-engine/)

[Memory Management in the APEX Engine - Digital Dragons 2022](https://gpuopen.com/videos/memory-management-in-the-apex-engine/)

[

This talk is a joint-presentation with Avalanche Studios Group explaining how their in-house APEX Engine manages memory with the help of VMA/D3D12MA.

](https://gpuopen.com/videos/memory-management-in-the-apex-engine/)

[![AMD Blender® USD™ Hydra™ Plug-in Overview - YouTube link](https://gpuopen.com/_astro/Blender-USD-video-thumbnail-1280px.D_mdDvKm_29kW57.jpg)](https://gpuopen.com/videos/hydra-blender-usd-video/)

[AMD Blender® USD™ Hydra™ Plug-in Overview - YouTube link](https://gpuopen.com/videos/hydra-blender-usd-video/)

[

This tutorial video demonstrates how to use our USD Hydra plug-in for Blender®, which uses the power of Open Standards to enable you to reference and assemble USD™, and use MaterialX.

](https://gpuopen.com/videos/hydra-blender-usd-video/)

[![Microsoft® Game Stack Live: AMD Ryzen Processor Software Optimization](https://gpuopen.com/_astro/gsl-video-ryzen.6WQVG7iT_1JfY1H.jpg)](https://gpuopen.com/videos/gsl-ryzen-optimization/)

[Microsoft® Game Stack Live: AMD Ryzen Processor Software Optimization](https://gpuopen.com/videos/gsl-ryzen-optimization/)

[

Join AMD on an adventure thru Zen 2 and Zen 3 processors which power today’s game consoles and PCs. Dive into instruction sets, cache hierarchies, resource sharing, and simultaneous multi-threading. Journey across the sands of silicon to master microarchitecture and uncover best practices!

](https://gpuopen.com/videos/gsl-ryzen-optimization/)

[![Microsoft® Game Stack Live: Denoising Raytraced Soft Shadows on Xbox Series X|S and Windows with FidelityFX](https://gpuopen.com/_astro/gsl-video-soft-shadows.O7JoJqhQ_Z1e5Dhf.jpg)](https://gpuopen.com/videos/gsl-denoising-soft-shadows/)

[Microsoft® Game Stack Live: Denoising Raytraced Soft Shadows on Xbox Series X|S and Windows with FidelityFX](https://gpuopen.com/videos/gsl-denoising-soft-shadows/)

[

We explain how FidelityFX Denoiser allows for high-quality raytracing results without increasing rays per pixel, and deep dive into specific AMD RDNA™ 2-based optimizations that benefit both Xbox Series X|S and PC.

](https://gpuopen.com/videos/gsl-denoising-soft-shadows/)

[![AMD RDNA™ 2 – DirectX® Raytracing 1.1 - YouTube link](https://gpuopen.com/_astro/rdna2-directxraytracing.CzVr0cgS_CvFvg.jpg)](https://gpuopen.com/videos/amd-rdna2-directx-raytracing/)

[AMD RDNA™ 2 – DirectX® Raytracing 1.1 - YouTube link](https://gpuopen.com/videos/amd-rdna2-directx-raytracing/)

[

Graphics feature architect Rys Sommefeldt provides a short presentation on the major advantages of the new API, and how to best utilize it on AMD RDNA™ 2-based hardware.

](https://gpuopen.com/videos/amd-rdna2-directx-raytracing/)