---
title: "how unreal engine upk files size compression works?"
source: "https://www.reddit.com/r/gameenginedevs/comments/1mp624o/how_unreal_engine_upk_files_size_compression_works/"
author:
  - "[[RKostiaK]]"
published: 2025-08-13
created: 2025-09-21
description:
tags:
  - "clippings"
---
im making my own file formats for texture and mesh in binary for my engine and achieved 9 mb for 140k vertices mesh.

i also looked at mirrors edge 1 made on unreal engine 3 and saw that there can be a upk file storing around 20 textures and the file is under 1 mb.

could anyone tell how unreal engine 3 did compressions on upk files, or atleast one of the methods that have the biggest effect?

---

## Comments

> **CptCap** • [3 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8hhvdh/) •
> 
> > a upk file storing around 20 textures and the file is under 1 mb.
> 
> This means nothing. Textures could be 16x16, in which case 1mb for 20 is very bad.
> 
> ---
> 
> Texture data is typically stored in BC1/4/7 in memory and compressed with a generic compression algorithm when on disk. BC1 is already pretty compact at 4 bits per pixel. Compressing that with something like LZ4 can reduce even more, although it really depends on the asset.
> 
> BC splits textures in 4x4 blocks which are stored individually. Blocks are often made of two parts (sometimes more for BC7) and compressing these two parts separately can increase the compression ratio quite a bit.
> 
> track me
> 
> > **RKostiaK** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8hugvs/) •
> > 
> > the 20 textures we like 1024 or 512 resolution, however im not sure if it actually stored in that 1mb or is the texture stored somewhere else and just referenced
> > 
> > > **CptCap** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8hx95g/) •
> > > 
> > > Don't compare yourself to unreal too much, especially when you have are not sure what you are even comparing. its a great way to get lost in the sauce and make no progress.
> > > 
> > > Using compact formats (like BC, or ASTC if you are on mobile) and compressing them on disk (using something like lz4 or zstd) will give you both good load times and decent size on disk.
> > > 
> > > I worked on two AAA engines and both did some variant of this.
> > > 
> > > *\[edit\]* you can also use files format like PNG. These will be more compact than compressed BC, but store RGB(A) data, so you won't get the VRAM saving of using BC. This is fine if you have little texture data, but will cause trouble in big scenes.
> > > 
> > > > **shadowndacorner** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8ijgtl/) •
> > > > 
> > > > > you can also use files format like PNG. These will be more compact than compressed BC
> > > > 
> > > > Why...? PNG is just deflate over an RGBA payload. Jpeg would have a better compression ratio because it's lossy, but BCn + zstd should theoretically get better compression because you're compressing less data with a better compression algorithm.
> > > > 
> > > > > **CptCap** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8jgqy7/) •
> > > > > 
> > > > > I said "like PNG" to mean general purpose image compression, but yes JPEG would work just as well and be smaller.
> > > > > 
> > > > > I would expect PNG to be better for non color data (like normals, roughness, ...). JPEG compression can cause some "cross-talk" between channels, which can be bad in this case.
> > > > > 
> > > > > > **shadowndacorner** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8jipq3/) •
> > > > > > 
> > > > > > To be clear, the point of my comment was just that PNG wouldn't be more highly compressed than BCn data with good lossless compression on top, because DEFLATE is pretty bad by modern standards and you'd be compressing an already smaller data set. Even aside from accuracy issues for non-color data, jpeg definitely isn't ideal for game assets if only because it needs to be first decoded into RGB data, then transformed into a GPU compressed format (including mips etc). I was just noting that it *could* be smaller because it's fundamentally different from PNG.
> > > > > > 
> > > > > > It's much better to just store a BCn payload w/ mips and compress it with zstd imo, even if the result is a bit bigger than a jpg, because it'll load significantly faster. LZ4 is even faster to load ofc, but its compression ratio is a good bit worse than zstd in my experience.
> > > > > > 
> > > > > > > **CptCap** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8k22nc/) •
> > > > > > > 
> > > > > > > > To be clear, the point of my comment was just that PNG wouldn't be more highly compressed than BCn data with good lossless compression on top
> > > > > > > 
> > > > > > > Oh ok! I expected deflate to be better than this. I guess not. Thanks for the head up.
> > > > > > > 
> > > > > > > > **shadowndacorner** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8k35gy/) •
> > > > > > > > 
> > > > > > > > Np! It's worth remembering that DEFLATE is almost 40 years old, and there has been a *lot* of innovation in the field since then.
> > > > > > > > 
> > > > > > > > Fwiw, DEFLATE has a slightly better compression ratio than LZ4, but is worse than zstd (both of which are significantly faster than DEFLATE). Brotli has the best compression ratio of any compression algos (at least as of a couple of years ago, which was the last time I benchmarked different compression algos against each other), but it's waaaay slower than zstd or LZ4.
> > > > > > > > 
> > > > > > > > In the context of games, imo LZ4hc is ideal for relatively small files that you want to load very quickly (it's barely slower than memcpy for decompression - it really is *wildly* fast), and zstd is good for everything else.
> > > > > > > > 
> > > > > > > > > **CptCap** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8k7y38/) •
> > > > > > > > > 
> > > > > > > > > Is zstd fast enough to be the default nowadays ?
> > > > > > > > > 
> > > > > > > > > I remember working on a X1/PS4 where the HDD was so slow than slower, stronger compression almost always meant faster loading. I would expect cheap SSD to have flipped the scale somewhat.
> > > > > > > > > 
> > > > > > > > > > **shadowndacorner** • [2 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8kq2hm/) •
> > > > > > > > > > 
> > > > > > > > > > I'll start by saying that everything is tradeoffs, and the effectiveness of compression will always be a function of the entropy of your data. If you have data with extremely high entropy, it doesn't matter which compression algorithm you use - it's going to be basically worthless. The lower your entropy, the more effective any compression algorithm will be, and the more attractive compressing that data is.
> > > > > > > > > > 
> > > > > > > > > > > Is zstd fast enough to be the default nowadays ?
> > > > > > > > > > 
> > > > > > > > > > In my experience, ***it depends***. It's a good default replacement for DEFLATE, but imo, LZ4hc tends to be a better "don't-think-too-hard-about-it" default for game content given its speed *unless* that content is particularly large and doesn't need to be streamed. For larger things that aren't streamed, I'd lean towards zstd for the better compression ratio. That being said, both are significantly faster than DEFLATE, so defaulting to Zstd will still be better than shipping PNGs :P
> > > > > > > > > > 
> > > > > > > > > > > I remember working on a X1/PS4 where the HDD was so slow than slower, stronger compression almost always meant faster loading. I would expect cheap SSD to have flipped the scale somewhat.
> > > > > > > > > > 
> > > > > > > > > > X1/PS4 had *awful* drives haha. When I last benchmarked, which was mostly against texture and texture-like data (LUTs, some baked data, etc) I had sitting around from various projects (along with a few pictures of my cat :P), uncompressed loads were faster compared to both LZ4hc and Zstd. Here's a table of averages I did from that testing using a Samsung 990 Pro, which includes the load time from disk...
> > > > > > > > > > 
> > > > > > > > > > |  | Uncompressed | LZ4 | LZ4HC | Zstd | Brotli |
> > > > > > > > > > | --- | --- | --- | --- | --- | --- |
> > > > > > > > > > |  |
> > > > > > > > > > | Load time (ms) | 11.868 | 15.164 | 13.706 | 27.498 | 40.26 |
> > > > > > > > > > | Size (mb) | 15.41 | 5.58 | 4.22 | 2.91 | 2.61 |
> > > > > > > > > > |  |  |  |  |  |  |
> > > > > > > > > > 
> > > > > > > > > > And on my 860 Evo...
> > > > > > > > > > 
> > > > > > > > > > |  | Uncompressed | LZ4 | LZ4HC | Zstd | Brotli |
> > > > > > > > > > | --- | --- | --- | --- | --- | --- |
> > > > > > > > > > |  |
> > > > > > > > > > | Load time (ms) | 13.09 | 15.77 | 14.578 | 27.896 | 40.13 |
> > > > > > > > > > | Size (mb) | 15.41 | 5.58 | 4.22 | 2.91 | 2.61 |
> > > > > > > > > > |  |  |  |  |  |  |
> > > > > > > > > > 
> > > > > > > > > > I unfortunately didn't have an old HDD to test against, but like your experience from Xbone/PS4, I would expect the uncompressed loads to be *much* slower than the either of the compressed loads in that case.
> > > > > > > > > > 
> > > > > > > > > > I'd stress that you shouldn't overgeneralize these results given the nature of the data. It's probably going to be more representative of the use cases in this sub compared to someone doing this kind of comparison for eg web content, but it's still fairly limited. A more complete benchmark would look at other kinds of data, but that wasn't super convenient given the context in which I was doing that benchmarking.
> > > > > > > > > > 
> > > > > > > > > > Of course, if you're targeting modern consoles, you should just use their hardware-accelerated formats, but I haven't benchmarked those. From what I understand, they are ***fantastic*** for their respective consoles since their IO stacks are built around them *and* they have dedicated decoding hardware for them, but it's much lower impact on PC. Iirc the Demon's Souls guys said that moving to the PS5's hardware Kraken decoder from RAD's software decoder took their load time down from the order of minutes to a few seconds, but don't quote me on those exact numbers - this was a long time ago haha. I mostly just remember that they were pretty amazed at the speed difference.

> **fgennari** • [1 points](https://reddit.com/r/gameenginedevs/comments/1mp624o/comment/n8hfqpj/) •
> 
> For the textures, simply using a compressed image format such as JPG (or PNG if you have RGBA or large areas of the same color) will give you good compression. Using other compression such as gzip won’t reduce the files much further. Mirror’s Edge probably had lower resolution textures and that’s how they fit all the data in 1MB.
> 
> I’m not familiar with UPK, but it’s likely a “pack” file format using similar ideas to Quake’s PAK files. It’s like a zip archive with a directory structure.