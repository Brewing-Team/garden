---
title: PARALLEL COMPUTING
source: https://gfxcourses.stanford.edu/cs149/fall25
author:
published:
created: 2026-03-03
description:
tags:
  - clippings
---
Stanford CS149, Fall 2025

PARALLEL COMPUTING

From smart phones, to multi-core CPUs, to GPUs, to AI accelerators, to the world's largest supercomputers and web sites, parallel processing is ubiquitous in modern computing. The goal of this course is to provide a deep understanding of the fundamental principles and engineering trade-offs involved in designing modern parallel computing systems as well as to teach parallel programming techniques necessary to effectively utilize these machines. Because writing good parallel programs requires an understanding of key machine performance characteristics, this course will cover both parallel hardware and software design.

Basic Info

Time: Tues/Thurs 10:30-11:50am

Location: NVIDIA Auditorium

Instructors: [Kayvon Fatahalian](http://graphics.stanford.edu/~kayvonf) and [Kunle Olukotun](https://engineering.stanford.edu/people/kunle-olukotun)

See the [course info](https://gfxcourses.stanford.edu/cs149/fall25/courseinfo) page for more info on policies and logistics.

Fall 2025 Schedule

| Sep 23 |  | [Why Parallelism? Why Efficiency?](https://gfxcourses.stanford.edu/cs149/fall25/lecture/efficiency/)  Challenges of parallelizing code, motivations for parallel chips, processor basics |
| --- | --- | --- |
| Sep 25 |  | [A Modern Multi-Core Processor (Part I)](https://gfxcourses.stanford.edu/cs149/fall25/lecture/multicore1/)  Forms of parallelism: multi-core, SIMD, and multi-threading |
| Sep 30 |  | [Modern Multi-Core Architecture (Part II) + ISPC Programming Abstractions](https://gfxcourses.stanford.edu/cs149/fall25/lecture/multicore2/)  Finish up multi-threaded and latency vs. bandwidth. ISPC programming, abstraction vs. implementation |
| Oct 02 |  | [Parallelizing Code: An Example Thought Process](https://gfxcourses.stanford.edu/cs149/fall25/lecture/thoughtprocess/) |
| Oct 07 |  | [Program Optimization 1: Work Distribution and Scheduling](https://gfxcourses.stanford.edu/cs149/fall25/lecture/perfopt1/)  Achieving good work distribution while minimizing overhead, scheduling Cilk programs with work stealing |
| Oct 09 |  | [Program Optimization 2: Locality and Communication](https://gfxcourses.stanford.edu/cs149/fall25/lecture/perfopt2/)  Message passing, async vs. blocking sends/receives, pipelining, increasing arithmetic intensity, avoiding contention |
| Oct 14 |  | [GPU Architecture and CUDA Programming](https://gfxcourses.stanford.edu/cs149/fall25/lecture/gpuarch/)  CUDA programming abstractions, and how they are implemented on modern GPUs |
| Oct 16 |  | [Data-Parallel Thinking](https://gfxcourses.stanford.edu/cs149/fall25/lecture/dataparallel/)  Data-parallel operations like map, reduce, scan, prefix sum, groupByKey |
| Oct 21 |  | [Efficiently Evaluating DNNs on GPUs: Transformers and ConvNets](https://gfxcourses.stanford.edu/cs149/fall25/lecture/dnninference/)  Efficiently scheduling DNN layers, mapping convs to matrix-multiplication, transformers, layer fusion |
| Oct 23 |  | [Hardware Specialization](https://gfxcourses.stanford.edu/cs149/fall25/lecture/accelerators/)  Energy-efficient computing, motivation for and design of hardware accelerators. Case study on DNN accelerator design. |
| Oct 28 |  | [Programming Systems for Specialized Hardware](https://gfxcourses.stanford.edu/cs149/fall25/lecture/proghardware/)  Modern trends and programming systems for creating specialized hardware |
| Oct 30 |  | [Mapping AI Applications to the Datacenter Computer](https://gfxcourses.stanford.edu/cs149/fall25/lecture/aidatacenter/)  How modern AI applications are served at datacenter scale |
| Nov 04 |  | Democracy Day (no class)  Attend Stanford's many events! |
| Nov 06 |  | [Domain-Specific Programming Systems and AI-Driven Performance Optimization](https://gfxcourses.stanford.edu/cs149/fall25/lecture/aiperfoptimization/)  Domain-specific programming abstractions for writing high-performance code, automatic program optimization, with a focus on optimization driven by AI agents |
| Nov 11 |  | [Cache Coherence](https://gfxcourses.stanford.edu/cs149/fall25/lecture/cachecoherence/)  Invalidation-based coherence using MSI and MESI, false sharing |
| Nov 13 |  | [Implementing Synchronization + Memory Consistency](https://gfxcourses.stanford.edu/cs149/fall25/lecture/sync_consistency/)  Fine-grained synchronization via locks, motivation for relaxed consistency, implications to programmers. |
| Nov 18 |  | Midterm Exam (no class)  This will be an evening exam, so there's no class |
| Nov 20 |  | [Fine-Grained Locking and Lock-Free Programming](https://gfxcourses.stanford.edu/cs149/fall25/lecture/finegrainedsync/)  Fine-grained synchronization via locks, basics of lock-free programming: single-reader/writer queues, lock-free stacks, the ABA problem |
| Dec 02 |  | [Transactional Memory (Part I)](https://gfxcourses.stanford.edu/cs149/fall25/lecture/transactions/)  Motivation for transactions, design space of transactional memory implementations, STM and HTM basics |
| Dec 04 |  | [Transactional Memory (Part II) + Ask Me Anything with Kunle and Kayvon](https://gfxcourses.stanford.edu/cs149/fall25/lecture/wrapup/)  Suggestions for post cs149 topics. AMA with the course staff. |
| Dec 11 |  | Final Exam  Held from 3:30-6:30pm |

Lecture Videos

We cannot distribute lecture videos to the public this year, but videos from a prior version of the course (2023) are available on [Stanford's Youtube Channel](https://www.youtube.com/playlist?list=PLoROMvodv4rMp7MTFr4hQsDEcX7Bx6Odp).

Programming Assignments

| Oct 6 | [Assignment 1: Analyzing Parallel Program Performance on a Quad-Core CPU](https://github.com/stanford-cs149/asst1) |
| --- | --- |
| Oct 16 | [Assignment 2: Scheduling Task Graphs on a Multi-Core CPU](https://github.com/stanford-cs149/asst2) |
| Oct 30 | [Assignment 3: A Circle Renderer in CUDA](https://github.com/stanford-cs149/asst3) |
| Nov 13 | [Assignment 4: Fused Conv+MaxPool on the Trainium2 Accelerator](https://github.com/stanford-cs149/asst4-trainium2) |
| Dec 4 | [Assignment 5: Make the World's Fastest CUDA Kernels](https://github.com/stanford-cs149/asst5-kernels) |

Written Assignments

| Oct 9 | [Written Assignment 1](https://gfxcourses.stanford.edu/cs149/fall25content/static/pdfs/written_asst1.pdf) |
| --- | --- |
| Oct 21 | [Written Assignment 2](https://gfxcourses.stanford.edu/cs149/fall25content/static/pdfs/written_asst2.pdf) |
| Nov 6 | [Written Assignment 3](https://gfxcourses.stanford.edu/cs149/fall25content/static/pdfs/written_asst3.pdf) |
| Dec 3 | [Written Assignment 4](https://gfxcourses.stanford.edu/cs149/fall25content/static/pdfs/written_asst4.pdf) |