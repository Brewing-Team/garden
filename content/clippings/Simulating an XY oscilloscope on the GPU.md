---
title: "Simulating an XY oscilloscope on the GPU"
source: "https://nicktasios.nl/posts/simulating-an-xy-oscilloscope-on-the-gpu.html"
author:
  - "[[Nick Tasios]]"
published: 2021-11-05
created: 2025-09-27
description: "It's been a couple of years since the post where I first introduced the new game I was working on, Vectron. In this post I wanted to tell you a bit about how I programmed the graphics of Vectron. Alth"
tags:
  - "clippings"
---
It's been a couple of years since the post where I first introduced the new game I was working on, Vectron. In this post I wanted to tell you a bit about how I programmed the graphics of Vectron. Although I finished the game nearly a year ago, I was putting of releasing it. Compiling it for Windows and MacOS was a barrier I had to overcome, but I can finally say that I released my first game! You can checkout Vectron's page on [itch.io](https://studiostok.itch.io/vectron).

## Vectron's graphics

![](https://www.youtube.com/watch?v=WcncEPcXbco)

After I worked out the basic gameplay elements of Vectron, I made some mood boards to help me determine the visual style I'd like to develop. In the end I wanted my game to have a visual style similar to the arcade game, [Tempest](https://en.wikipedia.org/wiki/Tempest_\(video_game\)), or the [Vectrex](https://en.wikipedia.org/wiki/Vectrex) and I was also greatly inspired by [video of Quake being played on an oscilloscope](https://www.youtube.com/watch?v=GIdiHh6mW58). This led me to doing some research on how the [Tempest was programmed](http://www.kfu.com/~nsayer/games/tempest.html), and how the beam in a CRT monitor works and interacts with the phosphors. Then, it was just a matter of time before I discovered the work of [Jerobeam Fenderson](https://www.youtube.com/user/jerobeamfenderson1), who is making music that looks amazing when displayed on an XY oscilloscope. I thus decided to base the design of my game around the concept of sound driving the graphics of the game and vice-versa.

## Oscilloscope basics

![](https://nicktasios.nl/files/Oscilloscope_sine_square.jpg)

An [oscilloscope](https://en.wikipedia.org/wiki/Oscilloscope) is a device that receives electrical signals as input and visualizes their variation over time on a screen. Modern oscilloscopes use an LCD display, but older ones used a [cathode ray tube](https://en.wikipedia.org/wiki/Cathode-ray_tube) (CRT), similar to older TVs. Typically they operate by periodically horizontally sweeping the CRT beam across the screen, while the voltage of the input signal determines the vertical position of the beam. The sweep frequency as well as the sensitivity of the vertical deflection to the voltage can be adjusted allowing it to display a multitude of signals. As a result of the phosphor layer on CRT, the beam leaves a glowing trail allowing the image to persist for a certain period between frequency sweeps.

Most oscilloscopes have a second input channel, Y, which can be used to control the horizontal deflection using an electrical signal, similar to how the X signal controls the vertical deflection. In this mode, time is not explicitly visualized, but only implicitly through the motion of the beam. In this mode, we can use the oscilloscope as a fancy, really fast Etch A Sketch. Let's first provide a constant 0 voltage signal to the Y channel, and provide a sinusoidal voltage signal to the X channel. If we make the frequency of the signal slow enough, we should be able to see the beam move back and forth like below.![](https://nicktasios.nl/files/oscilloscope_x_sine.gif) And if we pass a sinusoidal signal to the Y channel, we get the same motion in the vertical direction.![](https://nicktasios.nl/files/oscilloscope_y_sine.gif) Finally, we can pass both signals, and if we make the Y signal out of face with the X signal by π/2, we get a perfect circular motion.![](https://nicktasios.nl/files/oscilloscope_xy_circle.gif) As you can imagine, we can play with the signals we pass to the X and Y channels, and we literally draw anything, as long as we make the beam fast enough (by increasing the frequency of the signals) such that the phosphor on the screen doesn't have time to decay completely. Patterns formed in this way are known as [Lissajous curves](https://en.wikipedia.org/wiki/Lissajous_curve). In Vectron, one of the things I did was build a vocabulary of patterns including lines which can be used to build more complex patterns, such as polygons, etc.

## Beam Intensity

For rendering the oscilloscope beam, I based my work off of the nice blog post at [https://m1el.github.io/woscope-how/](https://m1el.github.io/woscope-how/). The basic assumption we make to easily and efficiently draw the oscilloscope beam is that between two points, the beam moves linearly. We basically linearly interpolate its position. For a beam from $(0,0)$ to $(l,0)$ , given that the intensity of the electron beam as a function of distance from its center follows a Gaussian distribution,
$$
I(d)=1σ2πe−d22σ2
$$
 the intensity of the beam at a position $p=(px,py)$ can be calculated according to m1el's post as,
$$
F(p)=12le−py22σ2[erf(pxσ2)−erf(px−lσ2)]
$$
 This was calculated by integrating the intensity of the electron beam along its linear path. We can improve m1el's result slightly by incorporating the phosphor decay as an exponential decay factor, $e−λ(Δt−t)$ , where $λ$ is the phosphor decay constant, and $Δt$ is the beam travel time. We further extend the integration to be over a piecewise linear path with $N$ linear segments and fix the time for each segment to $δt=Δt/N$ . Then, by integrating the amount of light that arrives at the point $p$ , over nth segment, we get,
$$
F(p)=e−(λNδ+py22σ2)σl2π∫nδt(n+1)δtdteλtexp⁡[−(px−l(t−nδt)/δt)22σ2]
$$
 which after feeding it to Wolfram Alpha, we get the following relatively complicated expression,
$$
(1)F(p)=δt2lexp⁡[(δtλσl2)2−δtλ(N−n−pxl)−py22σ2][erf(pxσ2+δtλσl2)−erf(px−lσ2+δtλσl2)]
$$
 As a side-note, at first I did not derive this complicated expression, but instead made an approximation by smoothly interpolating the decay factor along the beam path. If instead of interpolating the decay factor itself, we interpolate the decay factor exponent, we retrieve the following expression,
$$
F(p)=δt2lexp⁡[−δtλ(N−n−pxl)−py22σ2][erf(pxσ2)−erf(px−lσ2)]
$$
 which is the same as the more complex expressions with 
$$
δtλσl2=0.
$$
In practice, this is a reasonable assumption, and setting this expression to 0, does not affect the visual appearance unless the path is really short or the beam radius is really large.

## Implementation

In my implementation of the oscilloscope renderer, I draw a fixed number, N, of segments each frame. Furthermore, I use the frame time to multiply the whole frame with the exponential decay factor. I achieve this by using a [Frame Buffer Object (FBO)](https://en.wikipedia.org/wiki/Framebuffer_object), and alpha blending for multiplying by the decay factor. The rendering steps are then the following:

1. Bind the FBO.
2. Set the blend function to glBlendFunc(GL\_ONE\_MINUS\_SRC\_ALPHA, GL\_SRC\_ALPHA).
3. Render a full screen quad with a black color and alpha set to the decay factor, $e^{-\lambda \delta t N}$ .
4. Set the blend function to glBlendFunc(GL\_ONE, GL\_ONE).
5. Render beam segments.
6. Disable alpha blending.
7. Bind the draw buffer and draw the FBO texture to the screen (using SRGB).

Most of the steps are really simple and you can find out how to draw a fullscreen quad on other blog posts, such as [this one](https://nicktasios.nl/posts/space-invaders-from-scratch-part-2.html). For drawing the beam segments we actually use a trick that was described in m1el's post, namely we draw quads but instead of passing the coordinates of each corner, we only pass the coordinates of the segment endpoints, and generate the quad coordinates in the vertex shader based on their vertex id.![](https://nicktasios.nl/files/beam_segment_quad.svg) The implementation of the above trick can be seen in the vertex shader:

```
#version 330

layout(location = 0) in vec2 start;
layout(location = 1) in vec2 end;

// quad vertex ids
// 3--2
// | /|
// |/ |
// 0--1

uniform float beam_radius;
uniform vec2 aspect_ratio_correction;

flat out float path_length;
flat out int edge_id;
smooth out vec2 beam_coord;

void main(void)
{
    int vid = gl_VertexID % 4;
    path_length = length(end - start);

    vec2 dir = beam_radius * (
        (path_length > 1e-5)?
            (end - start) / path_length:
            vec2(1.0, 0.0)
    );

    vec2 orth = vec2(-dir.y, dir.x);
    vec2 pos =
        ((vid < 2)? start - dir: end + dir) +
       ((vid == 0 || vid == 3)? orth: -orth);

    pos *= aspect_ratio_correction;

    beam_coord.x = (
        (vid < 2)?
            -beam_radius:
            path_length + beam_radius
    );
    beam_coord.y = (
        (vid == 0 || vid == 3)?
            beam_radius:
            -beam_radius
    );

    edge_id = gl_VertexID / 4;

    gl_Position = vec4(pos, 0.0, 1.0);
}
```

Note that we pass `beam_coord` to the fragment shader with the keyword `smooth` so that it is interpolated over the quad. The fragment shader is a simple implementation of expression (1):

```
#version 330

#define SQRT2 1.4142135623730951
#define SQRT2PI 2.506628274631001

float erf(float x) {
    float s = sign(x), a = abs(x);
    x = 1.0 + (0.278393 + (0.230389 + 0.078108 * (a * a)) * a) * a;
    x *= x;
    return s - s / (x * x);
}

uniform vec3 beam_color;
uniform float beam_radius;
uniform float beam_dt;
uniform float beam_intensity;
uniform float beam_decay_time;
uniform uint beam_num_edges;

out vec4 outColor;

flat in float path_length;
flat in int edge_id;
smooth in vec2 beam_coord;

void main(void)
{
    float sigma = beam_radius / 5.0;
    float total_factor = beam_intensity * beam_dt;
    if(path_length > 1e-5)
    {
        float f = beam_dt * sigma /
            (SQRT2 * path_length * beam_decay_time);

        total_factor *=
            erf(f + beam_coord.x / (SQRT2 * sigma)) -
            erf(f + (beam_coord.x - path_length) / (SQRT2 * sigma));

        total_factor *= exp(
            f * f -
            beam_coord.y * beam_coord.y / (2.0 * sigma * sigma) -
            beam_dt * (
                float(beam_num_edges) -
                float(edge_id) -
                beam_coord.x / path_length
            ) / beam_decay_time
        ) / (2.0 * path_length);
    }
    else
    {
        total_factor *= exp(
            -dot(beam_coord, beam_coord) / (2.0 * sigma * sigma)
        ) / (SQRT2PI * sigma);
    }
    outColor = vec4(total_factor * beam_color, 1.0);
}
```

## Conclusion

Although you can make great games without being very good at math, or physics, here I was able to show you how leveraging math I could create a game with a unique graphics style. Although I've presented here the final renderer, my first approach was a really dumb CPU implementation where I explicitly (and inaccurately) performed the integral by drawing and accumulating a gaussian for each pixel in the beam's path. The results are actually not that bad as you can see below, and the performance is also better than you'd expect.![](https://nicktasios.nl/files/old_cpu_beam_renderer.png) Still, by constantly iterating on this idea, I was able to build something much more robust and performant. Despite that, there is still quite a bit room for improvement, such as reducing the overdraw by drawing a triangle strip, or reducing the number of required points, N, by using a better interpolation scheme than the linear interpolation we use now. The latter of course introduces additional complexity for calculating the relevant integrals.

Finally, the implementation of the oscilloscope input is also a very interesting story which I'd like to discuss next time. By introducing a vocabulary of input signals that can be combined in interesting ways, we can even build a simulation of a monochrome CRT monitor. The latter is something I'd like to explore more in the future, including the simulation of color CRT displays.

This is what I like about game programming; taking a simple idea and iterating on it. Playing with different ideas and researching the different possibilities, slowly gravitating to the ones you find the most interesting.