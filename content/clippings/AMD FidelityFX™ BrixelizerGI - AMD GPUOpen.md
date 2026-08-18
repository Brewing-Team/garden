---
title: AMD FidelityFX™ Brixelizer/GI - AMD GPUOpen
source: https://gpuopen.com/fidelityfx-brixelizer/
author:
published:
created: 2025-09-21
description: AMD FidelityFX™ Brixelizer GI is compute-based real-time dynamic global illumination solution built upon sparse distance fields.
tags:
  - clippings
  - global-illumination
---
![](https://gpuopen.com/_astro/brix-gi-headerimage_crop.BgywH8NX_Z2c8OXd.jpg)

Dynamic global illumination

AMD FidelityFX™ Brixelizer GI is a compute-based real-time dynamic global illumination solution built upon the sparse distance fields from AMD FidelityFX™ Brixelizer.

It provides you with denoised indirect diffuse and specular lighting outputs that you can composite into your final lighting output.

Supports:

- DirectX® 12
- Vulkan®

#### Part of the AMD FidelityFX™ SDK v1

[![AMD FidelityFX SDK components](https://gpuopen.com/_astro/FFX_SDK_banner-1024x570.BQkAdO3x_q1RqS.png)](https://gpuopen.com/amd-fidelityfx-sdk-1/)

This release of the AMD FidelityFX™ SDK adds the following features:

- AMD FidelityFX™ Brixelizer GI 1.0.1.
- Additions to the API and fixes for issues discovered.

[![Introducing AMD FidelityFX™ Brixelizer](https://gpuopen.com/_astro/featured-231937003-A_AMD_FidelityFX_Brixelizer_Lockup_RGB_Blk.DtyEKCn7_Z1KPGsb.png)](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

[Introducing AMD FidelityFX™ Brixelizer](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

[

As of FidelityFX SDK version 1.1, Brixelizer and Brixelizer GI are now unleashed to world so in this article we aim to discuss a few practical use cases and provide you with some tips you can apply for getting the most performance out of Brixelizer in your application.

](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

## Features

### State-of-the-art algorithm

### RDNA™-optimized

### Smart shader selection (SM 6.6+ when present)

### Open source, MIT license

### Easy to integrate

### Cross platform

### Details

AMD FidelityFX™ Brixelizer + Brixelizer GI features the following:

- Denoised indirect diffuse and indirect specular outputs
- Implemented in compute without hardware-accelerated ray-tracing
- Optional modes to output at lower than native resolutions
- AMD FidelityFX™ Brixelizer and Brixelizer GI sample code
- Native DirectX® 12 and Vulkan® SDK backend implementation libraries
- Fully dynamic global illumination with multiple bounces

For more information, don’t miss our [extensive documentation](https://gpuopen.com/manuals/fidelityfx_sdk/fidelityfx_sdk-index/).

## Algorithm overview - Brixelizer

AMD FidelityFX™ Brixelizer is a library that generates sparse distance fields for triangle geometry in real-time for efficiently tracing rays against your scene.

It works with both static and dynamic geometry and provides a shader API to trace rays against the distance field. It generates cascades of sparse distance fields around a given position and each cascade is split into 64x64x64 voxels.

If a voxel intersects any geometry, it generates a local distance field within the voxel. These local distance fields are known as Bricks.

![AMD FidelityFX™ Brixelizer diagram-1](https://gpuopen.com/_astro/brix-diagram-1.B4Murp56_1duSuR.jpg) *A top-down view of two AMD FidelityFX™ Brixelizer cascades containing geometry.*

![AMD FidelityFX™ Brixelizer diagram-2](https://gpuopen.com/_astro/brix-diagram-2.Da8U_ymw_2s9WaG.jpg) *A visualization of a slice from the brick atlas 3D texture.*

![AMD FidelityFX™ Brixelizer GI image](https://gpuopen.com/_astro/brix-gi-headerimage.BE8HH1rO_ZdFh7f.jpg) *Final lighting output of a 3D scene.*

![AMD FidelityFX™ Brixelizer SDF debug](https://gpuopen.com/_astro/fullsize_sdf-2.CW8QGKQr_ZbeR6E.jpg) *SDF debug visualization of a 3D scene.*

## Algorithm overview - Brixelizer GI

AMD FidelityFX™ Brixelizer GI is a simplified implementation of [AMD GI-1.0](https://gpuopen.com/learn/amd-capsaicin-framework-release-gi/).

It takes in the G-Buffer resources of your application alongside the output resources from AMD FidelityFX™ Brixelizer to generate Diffuse and Specular GI outputs.

![AMD FidelityFX™ Brixelizer GI diagram-1](https://gpuopen.com/_astro/high-level.BDvGhNzY_1OSSSV.jpg)

Due to the lack of material information in the distance field from AMD FidelityFX™ Brixelizer, we maintain an internal radiance cache which is populated by the previous frames’ lighting output.

Including just direct lighting will result in 1-bounce diffuse GI, whereas including the composited output from the previous frame gives you multiple bounces effectively for free.

*Left: Radiance cache with one bounce, right: Radiance cache with multiple bounces.*

Next we spawn screen probes on the visible surfaces in the depth buffer and shoot rays using AMD FidelityFX™ Brixelizer and sample the radiance cache for shading.

These screen probes are then used to feed a world space irradiance cache that stores spherical harmonics probes for each valid brick.

![AMD FidelityFX™ Brixelizer GI screen probes](https://gpuopen.com/_astro/fullsize_3-screen-probes.D8881XL6_Z2iyhzp.jpg) *Visualization of screen probes.*

![AMD FidelityFX™ Brixelizer GI irradiance cache](https://gpuopen.com/_astro/fullsize_3-irradiance-cache.BmsHxqVH_Z1jSxu3.jpg) *Visualization of the irradiance cache.*

Finally the outputs are resolved and denoised, leaving you with a Diffuse GI and Specular GI output that you can composite into your final lighting.

![AMD FidelityFX™ Brixelizer GI diffuse](https://gpuopen.com/_astro/fullsize_3-diffuse.DhFZa_yR_2eNqbn.jpg) *Denoised Diffuse GI output.*

![AMD FidelityFX™ Brixelizer GI specular](https://gpuopen.com/_astro/fullsize_3-specular.C5FUsT84_Z6olfj.jpg) *Denoised Specular GI output.*

![AMD FidelityFX™ Brixelizer GI final](https://gpuopen.com/_astro/fullsize_3-final.C5KDYwHd_N4vQ9.jpg) *Final lighting output with GI composited.*

## Additional resources

[![GDC 2024 - Global Illumination with AMD FidelityFX™ Brixelizer, plus AMD FidelityFX SDK updates - YouTube link](https://gpuopen.com/_astro/featured_Brixelizer_thumbnail.B_Es5mwk_aROMB.jpg)](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)

[GDC 2024 - Global Illumination with AMD FidelityFX™ Brixelizer, plus AMD FidelityFX SDK updates - YouTube link](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)

[

This talk briefly discusses how the AMD FidelityFX™ Brixelizer works, then explores how diffuse and specular global illumination is implemented with sparse distance fields in Brix GI.

](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)

[![Two-level radiance caching for fast and scalable real-time dynamic GI in games (GDC 2023 - YouTube link)](https://gpuopen.com/_astro/AGS-GI-Social.C4Ee7YdG_Kn5q9.jpg)](https://gpuopen.com/videos/two-level-radiance-caching-gi-gdc-2023/)

[Two-level radiance caching for fast and scalable real-time dynamic GI in games (GDC 2023 - YouTube link)](https://gpuopen.com/videos/two-level-radiance-caching-gi-gdc-2023/)

[

This presentation is a practical implementation of a solution aimed at making the most of every sample by caching the estimated radiance into a cache hierarchy used for both sampling and filtering.

](https://gpuopen.com/videos/two-level-radiance-caching-gi-gdc-2023/)

[![Real-time Sparse Distance Fields for Games (GDC 2023 - YouTube link)](https://gpuopen.com/_astro/Real-time-Sparse-Distance-Fields-Thumbnail-featured.5npMQq-W_1w6noY.jpg)](https://gpuopen.com/videos/gdc-2023-real-time-sparse-distance-fields-for-games/)

[Real-time Sparse Distance Fields for Games (GDC 2023 - YouTube link)](https://gpuopen.com/videos/gdc-2023-real-time-sparse-distance-fields-for-games/)

[

This presentation introduces a novel algorithm for PC and console developers to efficiently generate sparse distance fields in real-time.

](https://gpuopen.com/videos/gdc-2023-real-time-sparse-distance-fields-for-games/)

[![AMD FidelityFX™ Naming Guidelines in Game Titles](https://gpuopen.com/_astro/FidelityFX_Naming_Guidelines.BKuKl307_Z1yAOn3.jpg)](https://gpuopen.com/fidelityfx-naming-guidelines/)

[AMD FidelityFX™ Naming Guidelines in Game Titles](https://gpuopen.com/fidelityfx-naming-guidelines/)

[

A set of guidelines for developers on how to present options in the game’s user interface to enable/disable AMD FidelityFX Effects.

](https://gpuopen.com/fidelityfx-naming-guidelines/)

## Version history

### Other AMD FidelityFX effects

[![AMD FidelityFX™ Super Resolution 4 (FSR 4)](https://gpuopen.com/_astro/fullsize_fsr4-particles-full.DW_wtfEJ_S2qdA.jpg)](https://gpuopen.com/fidelityfx-super-resolution-4/)

[AMD FidelityFX™ Super Resolution 4 (FSR 4)](https://gpuopen.com/fidelityfx-super-resolution-4/)

[

AMD FSR 4 is our cutting-edge ML-based upscaler, part of AMD FidelityFX™ SDK v2. It delivers significant image quality improvements over FSR 3.1.

](https://gpuopen.com/fidelityfx-super-resolution-4/)

[![AMD FidelityFX™ Super Resolution 3 (FSR 3)](https://gpuopen.com/_astro/featured-FSR3-spaceship.CuTJZyM8_rhksO.jpg)](https://gpuopen.com/fidelityfx-super-resolution-3/)

[AMD FidelityFX™ Super Resolution 3 (FSR 3)](https://gpuopen.com/fidelityfx-super-resolution-3/)

[

Discover frame generation with AMD FidelityFX™ Super Resolution 3, and get the source code and documentation!

](https://gpuopen.com/fidelityfx-super-resolution-3/)

[![AMD FidelityFX™ Super Resolution 2 (FSR 2)](https://gpuopen.com/_astro/FFX_FSR_FSR2_2.D-N_B7Zd_qEUl5.jpg)](https://gpuopen.com/fidelityfx-superresolution-2/)

[AMD FidelityFX™ Super Resolution 2 (FSR 2)](https://gpuopen.com/fidelityfx-superresolution-2/)

[

Learn even more about our new open-source temporal upscaling solution FSR 2, and get the source code and documentation!

](https://gpuopen.com/fidelityfx-superresolution-2/)

[![AMD FidelityFX™ Super Resolution 1 (FSR 1)](https://gpuopen.com/_astro/fsr-source-previewcard.C4MFTVQL_ZD7hqv.jpg)](https://gpuopen.com/fidelityfx-superresolution/)

[AMD FidelityFX™ Super Resolution 1 (FSR 1)](https://gpuopen.com/fidelityfx-superresolution/)

[

AMD FidelityFX Super Resolution (FSR) is our open-source, high-quality, high-performance upscaling solution.

](https://gpuopen.com/fidelityfx-superresolution/)

[![AMD FidelityFX™ SDK v2](https://gpuopen.com/_astro/FidelityFX_SDK_featured.BztGQvfo_Z1kelvP.jpg)](https://gpuopen.com/amd-fidelityfx-sdk/)

[AMD FidelityFX™ SDK v2](https://gpuopen.com/amd-fidelityfx-sdk/)

[

AMD FidelityFX™ SDK v2 is the launchpad for our ML-based rendering technologies, inc. AMD FSR 4 and upcoming FSR Redstone features.

](https://gpuopen.com/amd-fidelityfx-sdk/)

[![AMD FidelityFX™ Breadcrumbs library](https://gpuopen.com/_astro/featured-breadcrumbs.CTafT2Yc_Z21T8kC.jpg)](https://gpuopen.com/fidelityfx-breadcrumbs/)

[AMD FidelityFX™ Breadcrumbs library](https://gpuopen.com/fidelityfx-breadcrumbs/)

[

AMD FidelityFX Breadcrumbs library uses the breadcrumbs marker technique to track down where your submitted commands cause a GPU crash.

](https://gpuopen.com/fidelityfx-breadcrumbs/)

[![AMD FidelityFX™ Lens](https://gpuopen.com/_astro/FFX_Lens.Ce55SH3Z_PGRwL.jpg)](https://gpuopen.com/fidelityfx-lens/)

[AMD FidelityFX™ Lens](https://gpuopen.com/fidelityfx-lens/)

[

AMD FidelityFX Lens is an AMD RDNA™ architecture optimized implementation of some of gaming''s most used post-processing effects.

](https://gpuopen.com/fidelityfx-lens/)

[![AMD FidelityFX™ Depth of Field (DoF)](https://gpuopen.com/_astro/FFX_DoF.ba0fiQDJ_udKbU.jpg)](https://gpuopen.com/fidelityfx-dof/)

[AMD FidelityFX™ Depth of Field (DoF)](https://gpuopen.com/fidelityfx-dof/)

[

AMD FidelityFX Depth of Field is an AMD RDNA™-architecture optimized implementation of physically correct camera-based depth of field.

](https://gpuopen.com/fidelityfx-dof/)

[![AMD FidelityFX™ SDK v1](https://gpuopen.com/_astro/featured_FFX_SDK.ClX_f8yH_Z1zPHLV.jpg)](https://gpuopen.com/amd-fidelityfx-sdk-1/)

[AMD FidelityFX™ SDK v1](https://gpuopen.com/amd-fidelityfx-sdk-1/)

[

The AMD FidelityFX SDK v1 is our easy-to-integrate solution for developers looking to include FidelityFX v1 features into their games.

](https://gpuopen.com/amd-fidelityfx-sdk-1/)

[![AMD FidelityFX™ Blur](https://gpuopen.com/_astro/FFX_Blur.CA4oX8Cc_ZkgrEb.jpg)](https://gpuopen.com/fidelityfx-blur/)

[AMD FidelityFX™ Blur](https://gpuopen.com/fidelityfx-blur/)

[

AMD FidelityFX Blur is an AMD RDNA™ architecture optimized collection of blur kernels from 3x3 up to 21x21.

](https://gpuopen.com/fidelityfx-blur/)

[![AMD FidelityFX™ Hybrid Stochastic Reflections sample](https://gpuopen.com/_astro/FFX_HybridReflections.BrXc0EK2_Z1tPQtM.jpg)](https://gpuopen.com/fidelityfx-hybrid-reflections/)

[AMD FidelityFX™ Hybrid Stochastic Reflections sample](https://gpuopen.com/fidelityfx-hybrid-reflections/)

[

This sample shows how to combine AMD FidelityFX Stochastic Screen Space Reflections (SSSR) with ray tracing in order to create high quality reflections.

](https://gpuopen.com/fidelityfx-hybrid-reflections/)

[![AMD FidelityFX™ Hybrid Shadows sample](https://gpuopen.com/_astro/FFX_HybridShadows_DebugRays.B9j3_0LC_Z1OzKO7.jpg)](https://gpuopen.com/fidelityfx-hybrid-shadows/)

[AMD FidelityFX™ Hybrid Shadows sample](https://gpuopen.com/fidelityfx-hybrid-shadows/)

[

This sample demonstrates how to combine ray traced shadows and rasterized shadow maps together to achieve high quality and performance.

](https://gpuopen.com/fidelityfx-hybrid-shadows/)

[![AMD FidelityFX™ Parallel Sort](https://gpuopen.com/_astro/fullsize_FFX_ParallelSort_featured.DE93yBTI_gkDhG.jpg)](https://gpuopen.com/fidelityfx-parallel-sort/)

[AMD FidelityFX™ Parallel Sort](https://gpuopen.com/fidelityfx-parallel-sort/)

[

AMD FidelityFX Parallel Sort makes sorting data on the GPU quicker, and easier. Use our SM6.0 compute shaders to get your data in order.

](https://gpuopen.com/fidelityfx-parallel-sort/)

[![AMD FidelityFX™ Variable Shading](https://gpuopen.com/_astro/FFX_VRS.CfMTpTwQ_1jTQdd.jpg)](https://gpuopen.com/fidelityfx-variable-shading/)

[AMD FidelityFX™ Variable Shading](https://gpuopen.com/fidelityfx-variable-shading/)

[

AMD FidelityFX Variable Shading drives Variable Rate Shading into your game.

](https://gpuopen.com/fidelityfx-variable-shading/)

[![AMD FidelityFX™ Denoiser](https://gpuopen.com/_astro/Featured_ShadowDenoiser.D_aP8dpN_14b9XW.jpg)](https://gpuopen.com/fidelityfx-denoiser/)

[AMD FidelityFX™ Denoiser](https://gpuopen.com/fidelityfx-denoiser/)

[

AMD FidelityFX Denoiser is a set of denoising compute shaders which remove artefacts from reflection and shadow rendering.

](https://gpuopen.com/fidelityfx-denoiser/)

[![AMD FidelityFX™ Luminance Preserving Mapper (HDR Mapper)](https://gpuopen.com/_astro/lpm_crop.CAxBAei3_iWHHu.jpg)](https://gpuopen.com/fidelityfx-lpm/)

[AMD FidelityFX™ Luminance Preserving Mapper (HDR Mapper)](https://gpuopen.com/fidelityfx-lpm/)

[

AMD FidelityFX LPM provides an open-source library to easily integrate HDR and wide gamut tone and gamut mapping into your game.

](https://gpuopen.com/fidelityfx-lpm/)

[![AMD FidelityFX™ Stochastic Screen Space Reflections (SSSR)](https://gpuopen.com/_astro/FFX_SSSR.CUUiW4-l_Hq2vi.jpg)](https://gpuopen.com/fidelityfx-sssr/)

[AMD FidelityFX™ Stochastic Screen Space Reflections (SSSR)](https://gpuopen.com/fidelityfx-sssr/)

[

The AMD FidelityFX SSSR effect provides an open-source library to easily integrate stochastic screen space reflections into your game.

](https://gpuopen.com/fidelityfx-sssr/)

[![AMD FidelityFX™ Combined Adaptive Compute Ambient Occlusion (CACAO)](https://gpuopen.com/_astro/FFX_Cacao.DvdzZd2b_Z235sc4.jpg)](https://gpuopen.com/fidelityfx-cacao/)

[AMD FidelityFX™ Combined Adaptive Compute Ambient Occlusion (CACAO)](https://gpuopen.com/fidelityfx-cacao/)

[

AMD FidelityFX Combined Adaptive Compute Ambient Occlusion (CACAO) is an AMD RDNA™ architecture optimized implementation of ambient occlusion.

](https://gpuopen.com/fidelityfx-cacao/)

[![AMD FidelityFX™ Single Pass Downsampler (SPD)](https://gpuopen.com/_astro/FFX_SPD.COxnqQ53_ZfuIPg.jpg)](https://gpuopen.com/fidelityfx-spd/)

[AMD FidelityFX™ Single Pass Downsampler (SPD)](https://gpuopen.com/fidelityfx-spd/)

[

AMD FidelityFX Single Pass Downsampler (SPD) provides an AMD RDNA™ architecture optimized solution for generating up to 12 MIP levels of a texture.

](https://gpuopen.com/fidelityfx-spd/)

[![AMD FidelityFX™ Cauldron Framework](https://gpuopen.com/_astro/featured_cauldron.B0hKhvLu_5mcI.jpg)](https://gpuopen.com/fidelityfx-cauldron-framework/)

[AMD FidelityFX™ Cauldron Framework](https://gpuopen.com/fidelityfx-cauldron-framework/)

[

AMD FidelityFX Cauldron Framework is our open-source experimentation framework for DirectX®12 and Vulkan®, provided in the AMD FidelityFX SDK.

](https://gpuopen.com/fidelityfx-cauldron-framework/)

[![AMD FidelityFX™ Contrast Adaptive Sharpening (CAS)](https://gpuopen.com/_astro/FFX_CAS.D7k1DdKX_Z2hAhf5.jpg)](https://gpuopen.com/fidelityfx-cas/)

[AMD FidelityFX™ Contrast Adaptive Sharpening (CAS)](https://gpuopen.com/fidelityfx-cas/)

[

AMD FidelityFX Contrast Adaptive Sharpening (CAS) provides a mixed ability to sharpen and optionally scale an image.

](https://gpuopen.com/fidelityfx-cas/)

### Related news and technical articles

[![Introducing AMD FidelityFX™ Brixelizer](https://gpuopen.com/_astro/featured-231937003-A_AMD_FidelityFX_Brixelizer_Lockup_RGB_Blk.DtyEKCn7_Z1KPGsb.png)](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

[Introducing AMD FidelityFX™ Brixelizer](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

[

As of FidelityFX SDK version 1.1, Brixelizer and Brixelizer GI are now unleashed to world so in this article we aim to discuss a few practical use cases and provide you with some tips you can apply for getting the most performance out of Brixelizer in your application.

](https://gpuopen.com/learn/getting-the-most-out-of-fidelityfx-brixelizer/)

[![Introducing the latest version of the AMD FidelityFX™ SDK - v1.1](https://gpuopen.com/_astro/featured-231937002-A_AMD_Fidelity_FX_SDK_Lockup_RGB_Blk.DQf2yosT_Zd3rQX.png)](https://gpuopen.com/learn/amd-fidelityfx-sdk-1-1/)

[Introducing the latest version of the AMD FidelityFX™ SDK - v1.1](https://gpuopen.com/learn/amd-fidelityfx-sdk-1-1/)

[

The AMD FidelityFX SDK v1.1 is now available. This update introduces three new FidelityFX™ technologies: FSR 3.1, Breadcrumbs, and BrixelizerGI.

](https://gpuopen.com/learn/amd-fidelityfx-sdk-1-1/)

[![GDC 2024: Work graphs, mesh shaders, FidelityFX™, dev tools, CPU optimization, and more.](https://gpuopen.com/_astro/GDC24-AMD.F-eOrhUs_ZF1ucN.jpg)](https://gpuopen.com/news/gdc-2024-announce/)

[GDC 2024: Work graphs, mesh shaders, FidelityFX™, dev tools, CPU optimization, and more.](https://gpuopen.com/news/gdc-2024-announce/)

[Our GDC 2024 presentations this year include work graphs, mesh shaders, AMD FSR 3, GI with AMD FidelityFX Brixelizer, AMD Ryzen optimization, RGD, RDTS, and GPU Reshape!](https://gpuopen.com/news/gdc-2024-announce/)

[![GDC 2023: Introducing the FidelityFX SDK with new technologies, an early look at FSR 3 + more!](https://gpuopen.com/_astro/AMD-GDC2023-SESSIONS.DcmuW4Eh_Z2l695c.jpg)](https://gpuopen.com/news/gdc-2023-fidelityfx-sdk-fsr3/)

### Related videos

[![GDC 2024 - Global Illumination with AMD FidelityFX™ Brixelizer, plus AMD FidelityFX SDK updates - YouTube link](https://gpuopen.com/_astro/featured_Brixelizer_thumbnail.B_Es5mwk_aROMB.jpg)](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)

[GDC 2024 - Global Illumination with AMD FidelityFX™ Brixelizer, plus AMD FidelityFX SDK updates - YouTube link](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)

[

This talk briefly discusses how the AMD FidelityFX™ Brixelizer works, then explores how diffuse and specular global illumination is implemented with sparse distance fields in Brix GI.

](https://gpuopen.com/videos/gdc-2024-global-illumination-with-brixelizer/)