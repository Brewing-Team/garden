---
title: Interactive Indirect Illumination Using Voxel Cone Tracing
source: https://research.nvidia.com/labs/rtr/publication/crassin2011givoxels/
author:
  - "[[Cyril Crassin]]"
published: 1899-12-31
created: 2025-09-21
description: Indirect illumination is an important element for realistic image synthesis, but its computation is expensive and highly dependent on the complexity of the scene and of the BRDF of the involved surfaces. While off-line computation and pre-baking can be acceptable for some cases, many applications (games, simulators, etc.) require real-time or interactive approaches to evaluate indirect illumination. We present a novel algorithm to compute indirect lighting in real-time that avoids costly precomputation steps and is not restricted to low-frequency illumination. It is based on a hierarchical voxel octree representation generated and updated on the fly from a regular scene mesh coupled with an approximate voxel cone tracing that allows for a fast estimation of the visibility and incoming energy. Our approach can manage two light bounces for both Lambertian and glossy materials at interactive framerates (25-70FPS). It exhibits an almost scene-independent performance and can handle complex scenes with dynamic content thanks to an interactive octree-voxelization scheme. In addition, we demonstrate that our voxel cone tracing can be used to efficiently estimate Ambient Occlusion.
tags:
  - clippings
  - global-illumination
---
### Abstract

Indirect illumination is an important element for realistic image synthesis, but its computation is expensive and highly dependent on the complexity of the scene and of the BRDF of the involved surfaces. While off-line computation and pre-baking can be acceptable for some cases, many applications (games, simulators, etc.) require real-time or interactive approaches to evaluate indirect illumination. We present a novel algorithm to compute indirect lighting in real-time that avoids costly precomputation steps and is not restricted to low-frequency illumination. It is based on a hierarchical voxel octree representation generated and updated on the fly from a regular scene mesh coupled with an approximate voxel cone tracing that allows for a fast estimation of the visibility and incoming energy. Our approach can manage two light bounces for both Lambertian and glossy materials at interactive framerates (25-70FPS). It exhibits an almost scene-independent performance and can handle complex scenes with dynamic content thanks to an interactive octree-voxelization scheme. In addition, we demonstrate that our voxel cone tracing can be used to efficiently estimate Ambient Occlusion.

Type

[Paper](https://research.nvidia.com/labs/rtr/publication/#0)

Publication

*Computer Graphics Forum (Pacific Graphics), 2011*

### Related

- [A Ray-Box Intersection Algorithm and Efficient Dynamic Voxel Rendering](https://research.nvidia.com/labs/rtr/publication/majercik2018raybox/)
- [The SGGX microflake distribution](https://research.nvidia.com/labs/rtr/publication/heitz2015sggx/)
- [Ray-aligned Occupancy Map Array for Fast Approximate Ray Tracing](https://research.nvidia.com/labs/rtr/publication/zeng2023ray/)
- [Real-Time Path Tracing and Beyond](https://research.nvidia.com/labs/rtr/publication/clarberg2022keynote/)
- [Research Advances Toward Real-Time Path Tracing](https://research.nvidia.com/labs/rtr/publication/clarberg2022gdc/)