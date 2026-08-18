---
title: "Slug Font Rendering Library"
source: "https://sluglibrary.com/"
author:
published:
created: 2026-04-20
description:
tags:
  - "clippings"
---
![Slug Library Logo](https://sluglibrary.com/slug.svg)

Dynamic GPU Font Rendering and Advanced Text Layout

![Slug GPU Font Rendering](https://sluglibrary.com/scene/tunnel.jpg)

**Slug** is a software library that has become the professional standard for rendering high-quality, resolution-independent text and vector graphics in 3D applications on the GPU. It can be used for drawing graphical user interfaces, rendering heads-up displays, showing debugging information, and placing text inside a 3D world or virtual environment.

![Slug Library Licensees](https://sluglibrary.com/logos.png)

| *“Slug was an easy choice for us because of its high-quality results, excellent runtime performance, ease of integration, and source access.”* —Zenimax Online | *“It’s super easy to integrate. Someone who hasn’t done gfx since fixed function pipeline got it working in our gfx code base in less than a day.”* —Blizzard |
| --- | --- |
| *“Slug is a great library that perfectly fits our needs.”* —Quantic Dream | *“For our upcoming title it will be a no-brainer to go with Slug.”* —Fatshark |

Slug renders shapes on the GPU directly from outline data composed of quadratic Bézier curves to produce crisp text at any scale or from any perspective. There are no precomputed texture images or signed distance fields. Slug uses a [breakthrough mathematical algorithm](http://jcgt.org/published/0006/02/02/), illustrated below, that we invented to achieve perfect robustness with high performance, and it is the *only* existing GPU method that renders properly antialiased glyphs with no artifacts under both magnification and minification.

Slug also provides text layout services that calculate the positions of the glyphs that are drawn for a given string of Unicode characters. In addition to basic bounding box and advance width calculations, it can perform kerning, ligature replacement, combining diacritical mark placement, character composition, and alternate substitution. More high-level information is available on the [Slug fact sheet](https://sluglibrary.com/slug.pdf).

Although Slug was originally designed only to render text, it can now draw generic vector graphics using the same technology. Complex diagrams and vector drawings can be rendered at blazingly fast speeds directly on the GPU with total resolution independence. We use these capabilities extensively in our [Radical Pie equation editor](https://radicalpie.com/), where Slug renders complex equations with attached drawings and annotations as well as the entire GUI.

The full set of features provided by Slug is described in the [Slug User Manual](https://sluglibrary.com/SlugManual.pdf).

[![The Slug Algorithm](https://sluglibrary.com/slug_algorithm.svg)](https://sluglibrary.com/slug_algorithm.pdf)

**[Get print version](https://terathon-software-llc.square.site/product/slug-poster/18)** (18 × 24 inch wall poster)

## Demo

A demo of the Slug library for Windows is available here:

**[Download Slug Demo](https://sluglibrary.com/SlugDemo.zip)**  
(Updated 31-Dec-2025)

The demo contains several pages of text and vector graphics that highlight rendering capabilities and typographic features. On most pages, left-clicking and dragging will scroll the scene, right-clicking and dragging will rotate the scene, and moving the mouse wheel will zoom in and out.

The text on the seventh page of the demo can be changed by placing a file named `story.txt` in the same folder as the demo application. This text file should be encoded as UTF-8, and up to 64 lines of it will be rendered in the demo. The font used for this text is `story.slug` in the `Fonts` folder. By default, this is just a copy of the Arial font, but you can change it by using the `slugfont` tool to import another `.ttf` or `.otf` file. To do so, copy the font file into the `Fonts` folder, and execute the following command line with the actual font name:

`slugfont <fontname> -o story.slug`

## Glyph Rendering

![](https://sluglibrary.com/glyph.png)

Each glyph is rendered by drawing a quad that covers its bounding box. (Because it’s only a box, it can be clipped or subdivided to match another surface inside a 3D environment.) A specialized shader efficiently determines how much each pixel inside the box is covered by the glyph using the original Bézier curve data stored in the font. Because no precomputed images or distance fields are involved, the result is a sharp outline at all resolutions with no faceting or blurring. Slug has the ability to apply a couple speed optimizations at large font sizes, one of which is rendering a tight bounding polygon instead of a plain box. The image to the right was rendered by Slug using Times New Roman at a 500-pixel font size.

![](https://sluglibrary.com/emoji.png)

In addition to boring old letters and numbers, Slug can render full-color emoji and pictographs with the same resolution independence that gives every contour a clean, crisp appearance at any scale. Slug supports the complete set of color characters defined by Unicode, and it can handle skin tone modifiers as well as zero-width joiner sequences.

The image to the left was rendered by Slug using the Segoe UI Emoji font at a 40-pixel size. This font ships with Windows and contains color layer data that elegantly provides the ability to scale multicolor emoji and pictographs with the same versatility as conventional black-and-white glyphs.

  

## Text Layout

Given a string of Unicode characters, Slug can lay out a line of text and produce the vertex data needed to render all of the corresponding glyphs. In the process, Slug can optionally apply kerning, ligature replacement, combining diacritical mark placement, and character composition. Slug also supports a number of OpenType features that include stylistic alternates, small caps, oldstyle figures, subscripts, superscripts, case-sensitive punctuation, and fractions.

| *Kerning* is a subtle process by which spacing between characters is adjusted to create a cleaner, more consistent appearance. In the image to the right, the top line is drawn without kerning, and the bottom line is drawn with kerning. Notice how the o and a are moved slightly to the left to fill in the empty space under the T and the W. Also, the period and closing quotation mark are moved in because there is space to do so. | ![](https://sluglibrary.com/kern.png) |
| --- | --- |
| Ligature replacement is the process by which a special glyph called a *ligature* is drawn in place of a specific sequence of two or more ordinary glyphs. This is often done for pairs of characters that frequently appear next to each other and tend to touch or overlap slightly. In the image to the right, ligatures for Th, fi, and ffl are provided by the font, and they are rendered as a total of three glyphs in the bottom line, whereas seven separate glyphs are rendered in the top line. | ![](https://sluglibrary.com/liga.png) |
| Unicode defines many different *combining marks* that are intended to be attached to the closest preceding base glyph. Combining marks can be attached to multiple points on a base glyph or even to other combining marks at specific locations defined by the font. This allows accents and other types of symbols to be drawn with characters that may not have a precomposed equivalent in Unicode. The image to the right shows several combining marks that are automatically placed in the right position and stacked on top of each other. | ![](https://sluglibrary.com/mark.png) |
| Some fonts, especially those that contain emoji, define *character composition* sequences that allow specific groups of glyphs to be replaced by new glyphs that represent the meanings of those sequences. Unicode defines a set of skin tone modifiers and zero-width joiner sequences that rely on this feature. In the image to the right, the top line shows the individual glyphs before composition, and the bottom line shows the composed glyphs that replace those sequences. | ![](https://sluglibrary.com/join.png) |

## The Product

Slug is distributed as a static library that has a basic C++ interface, and full source is included with every license. Slug is platform agnostic and runs on Windows, Mac, Linux, iOS, Android, and all major game consoles. It can be used with Vulkan, Direct3D 10/11/12, OpenGL 3.0–4.6, Metal, and WebGL2. The API is fully documented in the [Slug User Manual](https://sluglibrary.com/SlugManual.pdf).

The primary function of Slug is to take a Unicode string (encoded as UTF-8), lay out the corresponding glyphs, and generate a vertex buffer containing the data needed to draw them. When text is rendered, your application binds the vertex buffer, one of our glyph shaders, and two texture maps associated with the font. One texture holds all of the Bézier curve data, and the other texture holds spatial data structures that Slug uses for efficient rendering.

Slug can render each glyph as a single quad. This has the advantage that it’s easy to clip to an irregular shape or project onto a curved surface in a 3D environment. It also means that vertex buffer storage requirements do not depend on the complexity of the glyphs. There is also an optimization that uses a tighter polygon having between three and six vertices that can be enabled to increase speed at moderate and large font sizes.)

Slug comes with a standalone tool that reads both the TrueType and PostScript flavors of the OpenType format (having `.ttf` and `.otf` file extensions, respectively) and generates a new file with the `.slug` extension containing all of the information necessary to render the font on the GPU. The `.slug` file includes the original glyph outline data, optimization data used by the glyph shader, kerning data, join sequence data, mark attachment data, and color layer data. A `.slug` file may contain a subset of the original font so that unneeded characters do not take up any space. The data used for kerning, join sequences, mark attachments, and color layers is all optional.

The technical details about how the Slug algorithm works and how the data is organized in `.slug` files are discussed in a paper by Eric Lengyel in the [Journal of Computer Graphics Techniques](http://jcgt.org/published/0006/02/02/). There is also a detailed [slide presentation](http://terathon.com/i3d2018_lengyel.pdf) about the Slug algorithm.

## Licensing

We have many flexible licensing options available for a wide range of applications and budgets. Slug can be licensed on a per-title basis, or it can be licensed once for every product you make until the end of time. Our support options range from questions over email to an on-site visit from the guy who actually built the thing. We’re open to negotiating any other reasonable terms as well. We recognize that many situations are unique, and we are prepared to tailor a license specifically to your company’s needs. Please [contact us](mailto:info@terathon.com) to get the ball rolling.

For **individuals**, we have a single-engineer license for a one-time cost of $1500 (USD). This license includes the full source code for the Slug Library and associated tools, it allows usage in an unlimited number of commercial products, and it includes all future updates at no additional cost as long as you’re solo. If you’re interested in this license, please [contact us](mailto:info@terathon.com), and we will set you up.

## Why the name “Slug”?

The name Slug comes from the history of typography. A full line of text cast as one piece of hot lead by a [Linotype machine](https://en.wikipedia.org/wiki/Linotype_machine) was called a *slug*. The primary function of our software is to lay out and render lines of text.