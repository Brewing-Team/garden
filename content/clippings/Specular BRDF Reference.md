---
title: "Specular BRDF Reference"
source: "https://graphicrants.blogspot.com/2013/08/specular-brdf-reference.html"
author:
  - "[[Brian Karis]]"
published: 2013-08-04
created: 2025-09-27
description: ""
tags:
  - "clippings"
---
$$
\newcommand{\nv}{\mathbf{n}}
\newcommand{\lv}{\mathbf{l}}
\newcommand{\vv}{\mathbf{v}}
\newcommand{\hv}{\mathbf{h}}
\newcommand{\mv}{\mathbf{m}}
\newcommand{\rv}{\mathbf{r}}

\newcommand{\ndotl}{\nv\cdot\lv}
\newcommand{\ndotv}{\nv\cdot\vv}
\newcommand{\ndoth}{\nv\cdot\hv}
\newcommand{\ndotm}{\nv\cdot\mv}
\newcommand{\vdoth}{\vv\cdot\hv}
$$
 While I worked on our [new shading model for UE4](http://blog.selfshadow.com/publications/s2013-shading-course/) I tried many different options for our specular BRDF. Specifically, I tried many different terms for to Cook-Torrance microfacet specular BRDF:Directly comparing different terms requires being able to swap them while still using the same input parameters. I thought it might be a useful reference to put these all in one place using the same symbols and same inputs. I will use the same form as Naty \[1\], so please look there for background and theory. I'd like to keep this as a living reference so if you have useful additions or suggestions let me know.  
  
First let me define alpha that will be used for all following equations using UE4's roughness:  

## Normal Distribution Function (NDF)

The NDF, also known as the specular distribution, describes the distribution of microfacets for the surface. It is normalized \[12\] such that:It is interesting to notice all models have for the normalization factor in the isotropic case.  
  

---

**Blinn-Phong \[2\]:**This is not the common form but follows when .  

---

**Beckmann \[3\]:**  

---

**GGX (Trowbridge-Reitz) \[4\]:**  

---

**GGX Anisotropic \[5\]:**  

---

  

## Geometric Shadowing

The geometric shadowing term describes the shadowing from the microfacets. This means ideally it should depend on roughness and the microfacet distribution.  

---

**Implicit \[1\]:**  

---

**Neumann \[6\]:**  

---

**Cook-Torrance \[11\]:**  

---

**Kelemen \[7\]:**  

---

  

### Smith

The following geometric shadowing models use Smith's method\[8\] for their respective NDF. Smith breaks into two components: light and view, and uses the same equation for both:I will define below for each model and skip duplicating the above equation.  
  

---

**Beckmann \[4\]:**  

---

**Blinn-Phong:**  
The Smith integral has no closed form solution for Blinn-Phong. Walter \[4\] suggests using the same equation as Beckmann.  
  

---

**GGX \[4\]:**This is not the common form but is a simple refactor by multiplying by .  
  

---

**Schlick-Beckmann:**  
Schlick \[9\] approximated the Smith equation for Beckmann. Naty \[1\] warns that Schlick approximated the wrong version of Smith, so be sure to compare to the Smith version before using.  

---

**Schlick-GGX:**  
For UE4, I used the Schlick approximation and matched it to the GGX Smith formulation by remapping \[10\]:  

---

  

## Fresnel

The Fresnel function describes the amount of light that reflects from a mirror surface given its index of refraction. Instead of using IOR we instead use the parameter or which is the reflectance at normal incidence.  
  

---

**None:**  

---

**Schlick \[9\]:**  

---

**Cook-Torrance \[11\]:**  

---

  

## Optimize

Be sure to optimize the BRDF shader code as a whole. I choose these forms of the equations to either match the literature or to demonstrate some property. They are not in the optimal form to compute in a pixel shader. For example, grouping Smith GGX with the BRDF denominator we have this:In optimized HLSL it looks like this:  
  
float a2 = a\*a;  
float G\_V = NoV + sqrt( (NoV - NoV \* a2) \* NoV + a2 );  
float G\_L = NoL + sqrt( (NoL - NoL \* a2) \* NoL + a2 );  
return rcp( G\_V \* G\_L );  
  
If you are using this on an older non-scalar GPU you could vectorize it as well.  
  

### References

\[1\] Hoffman 2013, ["Background: Physics and Math of Shading"](http://blog.selfshadow.com/publications/s2013-shading-course/)  
\[2\] Blinn 1977, "Models of light reflection for computer synthesized pictures"  
\[3\] Beckmann 1963, "The scattering of electromagnetic waves from rough surfaces"  
\[4\] Walter et al. 2007, ["Microfacet models for refraction through rough surfaces"](http://www.cs.cornell.edu/~srm/publications/EGSR07-btdf.pdf)  
\[5\] Burley 2012, ["Physically-Based Shading at Disney"](http://blog.selfshadow.com/publications/s2012-shading-course/)  
\[6\] Neumann et al. 1999, ["Compact metallic reflectance models"](http://sirkan.iit.bme.hu/~szirmay/brdf6.pdf)  
\[7\] Kelemen 2001, ["A microfacet based coupled specular-matte brdf model with importance sampling"](http://sirkan.iit.bme.hu/~szirmay/scook.pdf)  
\[8\] Smith 1967, "Geometrical shadowing of a random rough surface"  
\[9\] Schlick 1994, ["An Inexpensive BRDF Model for Physically-Based Rendering"](http://www.cs.virginia.edu/~jdl/bib/appearance/analytic%20models/schlick94b.pdf)  
\[10\] Karis 2013, ["Real Shading in Unreal Engine 4"](http://blog.selfshadow.com/publications/s2013-shading-course/karis/s2013_pbs_epic_notes.pdf)  
\[11\] Cook and Torrance 1982, ["A Reflectance Model for Computer Graphics"](http://graphics.pixar.com/library/ReflectanceModel/)  
\[12\] Reed 2013, ["How Is the NDF Really Defined?"](http://www.reedbeta.com/blog/2013/07/31/hows-the-ndf-really-defined/)