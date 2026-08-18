---
title: "Approaching zero driver overhead"
source: "https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457"
author:
  - "[[CCass EverittSeguir]]"
published: 2014-03-20
created: 2025-05-27
description: "Approaching zero driver overhead - Descargar como PDF o ver en línea de forma gratuita"
tags:
  - "clippings"
---

[1 ![Approaching Zero
Driver Overhead
Cass Everitt
NVIDIA
Tim Foley
Intel
Graham Sellers
AMD
John McDonald
NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-1-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#1) 

[2 ![Cass Everitt
● NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-2-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#2) Lo más leído

[3 ![Assertion
● OpenGL already has paths with very low
driver overhead
● You just need to know
● What they are, and
● How to use them
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-3-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#3) 

[4 ![But first, who are we?
● Graham Sellers @GrahamSellers
● AMD OpenGL driver manager, OpenGL SuperBible author
● Tim Foley @TangentVector
● Graphics researcher, GPU language/compiler nerd
● John McDonald @basisspace
● Graphics engineer, chip architect, game developer
● Cass Everitt @casseveritt
● GL zealot, chip architect, mobile enthusiast
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-4-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#4) 

[5 ![Many kinds of bottlenecks
● Focus here is ―driver limited‖
● App could render more, and
● GPU could render more, but
● Driver is at its limit…
● Because of expensive API calls
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-5-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#5) 

[6 ![Some causes of driver overhead
● The CPU cost of fulfilling the
API contract
● Validation
● Hazard avoidance
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-6-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#6) 

[7 ![Costs that add up…
● Major Categories:
● synchronization, allocation,
validation, and compilation
● Buffer updates (synchronization, allocation)
● Mapping, in-band updates
● Binding objects (validation, compilation)
● FBOs, programs, textures, buffers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-7-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#7) 

[8 ![Remedy? – Efficient APIs!
● Buffer storage
● Texture arrays
● Multi-Draw Indirect
● Texture arrays, bindless,
sparse, indirect parameters
}Tim Foley
Graham Sellers}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-8-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#8) 

[9 ![Results
● apitest
● Framework for testing
different ―solutions‖
● Source on github
}John McDonald
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-9-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#9) 

[10 ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and
mostly core (GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-10-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#10) 

[11 ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and mostly core
(GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-11-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#11) 

[12 ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and mostly
core (GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-12-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#12) 

[13 ![On with the show…
next speaker
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-13-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#13) 

[14 ![Tim Foley
● Intel
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-14-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#14) 

[15 ![Challenge: More Stuff per Frame
● Varied
● Not 1000s of same instanced mesh
● Unique geometry, textures, etc.
● Dynamic
● Not just pretty skinned meshes
● Generate new geometry each frame
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-15-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#15) 

[16 ![Want an Order of Magnitude
● Increase in unique objects per frame
● Can over-simplify as draws per frame, but
● Misses importance of variety
● Do we need a new API to achieve this?
● How far can we get with what we have today?
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-16-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#16) 

[17 ![Three Techniques in This Talk
● Persistent-mapped buffers
● Faster streaming of dynamic geometry
● MultiDrawIndirect (MDI)
● Faster submission of many draw calls
● Packing 2D textures into arrays
● Texture changes no longer break batches
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-17-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#17) 

[18 ![Naïve Draw Loop
foreach( object )
{
// bind framebuffer
// set depth, blending, etc. states
// bind shaders
// bind textures
// bind vertex/index buffers
WriteUniformData( object );
glDrawElements(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
0 );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-18-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#18) 

[19 ![Typical Draw Loop
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-19-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#19) 

[20 ![Two Ways to Improve Overhead
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
submit each batch faster
fewer, bigger batches
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-20-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#20) 

[21 ![Pack Multiple Objects per Buffer
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
pack multiple objects into the same
(dynamic or static) vertex/index buffer
take advantage of glDraw*() params to
index into buffer without changing
bindings
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-21-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#21) 

[22 ![Dynamic Streaming of Geometry
● Typical dynamic vertex ring buffer
void* data = glMapBuffer(GL_ARRAY_BUFFER,
ringOffset,
dataSize,
GL_MAP_UNSYNCHRONIZED_BIT
| GL_MAP_WRITE_BIT );
WriteGeometry( data, ... );
glUnmapBuffer(GL_ARRAY_BUFFER);
ringOffset += dataSize;
// deal with wrap-around in ring, etc.
frequent mapping = overhead
no sync with GPU, but forces
sync in multi-threaded drivers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-22-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#22) 

[23 ![BufferStorage and Persistent Map
● Allocate buffer with glBufferStorage()
● Use flags to enable persistent mapping
glBufferStorage(GL_ARRAY_BUFFER, ringSize, NULL, flags);
GLbitfield flags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
keep mapped while drawing
writes automatically visible to GPU
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-23-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#23) Lo más leído

[24 ![Dynamic Streaming of Geometry
● Map once at creation time
● No more Map/Unmap in your draw loop
● But need to do synchronization yourself
data = glMapBufferRange(ARRAY_BUFFER, 0, ringSize, flags);
WriteGeometry( data, ... );
data += dataSize;
upcoming talks will cover
glFenceSync() and glClientWaitSync()
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-24-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#24) 

[25 ![Performance
● BufferSubData vs Map(UNSYNCHRONIZED)
● Intel: avoid frequent BufferSubData()
● NV: Map(UNSYNCH) bad for threaded drivers
● Persistent mapping best where supported
● Overhead 2-20x better than next best option
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-25-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#25) 

[26 ![That Inner Loop Again
foreach( object )
{
WriteUniformData( object, &uniformData );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-26-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#26) 

[27 ![Using an Indirect Draw
DrawElementsIndirectCommand command;
foreach( object )
{
WriteUniformData( object, &uniformData );
WriteDrawCommand( object, &command );
glDrawElementsIndirect(
GL_TRIANGLES,
GL_UNSIGNED_SHORT,
&command );
}
typedef struct {
uint count;
uint instanceCount;
uint firstIndex;
uint baseVertex;
uint baseInstance;
} DrawElementsIndirectCommand;
per-object parameters are
now sourced from memory
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-27-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#27) 

[28 ![One Multi-Draw Submits it All
DrawElementsIndirectCommand* commands = ...;
foreach( object )
{
WriteUniformData( object, &uniformData[i] );
WriteDrawCommand( object, &commands[i] );
}
glMultiDrawElementsIndirect(
GL_TRIANGLES,
GL_UNSIGNED_SHORT,
commands,
commandCount,
0 );
fill in per-object data
(use parallelism, GPU compute if you like)
kick buffered-up objects to be rendered
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-28-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#28) 

[29 ![What if I don‘t know the count?
● Doing GPU culling, etc.
● Use ARB_indirect_parameters
● Caveat: not all HW/drivers support it
glBindBuffer( GL_DRAW_INDIRECT_BUFFER, commandBuffer );
glBindBuffer( GL_PARAMETER_BUFFER, countBuffer );
// …
glMultiDrawElementsIndirectCount(
GL_TRIANGLES, GL_UNSIGNED_SHORT,
commandOffset,
countOffset,
maxCommandCount,
0 );
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-29-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#29) 

[30 ![Per-Draw Parameters/Data
● If shader used to take struct of uniforms
● Now take an array of such structs
● Or use SSBO to go bigger
uniform ShaderParams params;
(Shader Storage Buffer Object)
uniform ShaderParams params[MAX_BATCH_SIZE];
buffer AllTheParams { ShaderParams params[]; };
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-30-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#30) 

[31 ![How to find your draw‘s data?
● Ideally, just index it using gl_DrawID
● Provided by ARB_shader_draw_parameters
● Not supported everywhere
● But relatively simple to implement your own
mat4 mvp = params[gl_DrawIDARB].mvp;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-31-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#31) 

[32 ![Implement Your Own Draw ID
● Use baseInstance field of draw struct
● Increment base instance for each command
● Shader can‘t see base instance
● gl_InstanceID always counts from zero
http://www.g-truc.net/post-0518.html
cmd->baseInstance = drawCounter++;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-32-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#32) Lo más leído

[33 ![Implement Your Own Draw ID
● Use a vertex attribute
● Set as per-instance with glVertexAttribDivisor
● Fill buffer with your own IDs
● Or arbitrary other per-draw parameters
● On some HW, faster than using gl_DrawID
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-33-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#33) 

[34 ![More MultiDrawIndirect Caveats
● If generating draws on GPU
● Use a GL buffer (obviously)
● If generating on CPU
● Intel: (Compat) faster to use ordinary host pointer
● NV: persistent-mapped buffer slightly faster
● GPU or CPU
● AMD: Array must be tightly packed for best perf
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-34-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#34) 

[35 ![Can Be 6-10x Less Overhead
0%
100%
200%
300%
400%
500%
600%
700%
Dynamic Buffer Persistent-Mapped Multi-Draw
Normalized Objects per Second
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-35-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#35) 

[36 ![Batching Across Texture Changes
● Bindless, sparse can help
● As you will hear
● Not all hardware supports these
● Packing 2D textures into arrays
● Works on all current hardware/drivers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-36-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#36) 

[37 ![Packing Textures Into Arrays
● Array groups textures with same shape
● Dimensions, format, mips, MSAA
● Texture views may allow further grouping
● Put some same-size formats together
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-37-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#37) 

[38 ![Packing Textures Into Arrays
● Bind all arrays to pipeline at once
● Need to allocate carefully
● Based on your content requirements
● Don‘t allocate more than fits in GPU memory
uniform sampler2Darray allSamplers[MAX_ARRAY_TEXTURES];
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-38-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#38) 

[39 ![Options for Sampler Parameters
● Pair array with different sampler objs
● Create views of array with different state
● Be careful about max texture limits
● Each combination needs a new binding slot
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-39-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#39) 

[40 ![Accessing Packed 2D Textures
● Texture ―handle‖ is pair of indices
● Index into array of sampler2Darray
● Slice index into particular array texture
● Can store as 64 bits {int;float;}
● Or pack into 32 bits (hi/lo) no int→float convert in shader
fewer bytes to read, but more math
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-40-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#40) 

[41 ![Texture Array ~5x Less Overhead
0%
100%
200%
300%
400%
500%
600%
glBindTexture per Object Texture Arrays No Texture
Normalized Objects per Second
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-41-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#41) 

[42 ![Dramatically Reduced Overhead
● Possible with current GL API and HW
● Persistent-mapped buffers
● Indirect and Multi-Draws
● Packing 2D textures into arrays
● Overhead is priority for all of us on GL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-42-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#42) 

[43 ![Graham Sellers
● AMD
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-43-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#43) 

[44 ![Section Overview
● Bindless textures
● Recap of traditional texture binding
● Remove texture units with bindless
● Sparse textures
● Manage virtual and physical memory
● Streaming, sparse data sets, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-44-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#44) 

[45 ![Texture Units - Recap
● Traditional texture binding
● Create textures
● Bind to texture units
● Declare samplers in shaders
● Draw
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-45-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#45) 

[46 ![Texture Units - Recap
● Textures bound to numbered units
● Limited number of texture units
● State changes between draws
● Driver controls residency
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-46-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#46) 

[47 ![Texture Units - Recap
● Binding textures - API
● Very hard to coalesce draws
glGenTextures(10, &tex[0]);
glBindTexture(GL_TEXTURE_2D, tex[n]);
glTexStorage2D(GL_TEXTURE_2D, ...);
foreach (draw in draws) {
foreach (texture in draw->textures) {
glBindTexture(GL_TEXTURE_2D, tex[texture]);
}
// Other stuff
glDrawElements(...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-47-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#47) 

[48 ![Texture Units - Recap
● Binding textures - shader
● Limited textures per shader
● All declared at global scope
layout (binding = 0) uniform sampler2D uTexture1;
layout (binding = 1) uniform sampler3D uTexture2;
out vec4 oColor;
void main(void){
oColor = texture(uTexture1, ...) +
texture(uTexture2, ...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-48-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#48) 

[49 ![Bindless Textures
● Remove texture bindings!
● Unlimited* virtual texture bindings
● Application controls residency
● Shader accesses textures by handle
* Virtually unlimited
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-49-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#49) 

[50 ![Bindless Textures
● Bindless textures - API
● No texture binds between draws
// Create textures as normal, get handles from textures
GLuint64 handle = glGetTextureHandleARB(tex);
// Make resident
glMakeTextureHandleResidentARB(handle);
// Communicate ‘handle’ to shader... somehow
foreach (draw) {
glDrawElements(...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-50-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#50) 

[51 ![Bindless Textures
● Bindless textures - shader
● Shader accesses textures by handle
● Must communicate handles to shader
uniform Samplers {
sampler2D tex[500]; // Limited only by storage
};
out vec4 oColor;
void main(void) {
oColor = texture(tex[123], ...) + texture(tex[456], ...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-51-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#51) 

[52 ![Bindless Textures
● Handles are 64-bit integers
● Stick them in uniform buffers
● Switch set of textures – glBindBufferRange
● Number of accessible textures limited by buffer size
● Put them in structures (AoS)
● Index with gl_DrawIDARB, gl_InstanceID
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-52-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#52) 

[53 ![Bindless Textures – DANGER!!!
● Some caveats with bindless textures
● Divergence rules apply
● Just like indexing arrays of textures
● Bindless handle must be constant across instance
● Divergence might work
● On some implementations, it Just Works
● On others, it Just Doesn‘t
● Even when it works, it could be expensive
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-53-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#53) 

[54 ![Sparse Textures
● Very large virtual textures
● Separate virtual and physical allocation
● Partially populated arrays, mips, cubes, etc.
● Stream data on demand
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-54-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#54) 

[55 ![Sparse Textures
● Textures arranged as tiles
● Each tile may be resident or not
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-55-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#55) 

[56 ![Sparse Textures
● Sparse textures – API
● That‘s it – now you have a virtual texture
// Tell OpenGL you want a sparse texture
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_SPARSE_ARB, GL_TRUE);
// Allocate storage
glTexStorage2D(GL_TEXTURE_2D, 10, GL_RGBA8, 1024, 1024);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-56-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#56) 

[57 ![Sparse Textures
● Sparse textures – page sizes
// Query number of available page sizes
glGetInternalformativ(GL_TEXTURE_2D, GL_NUM_VIRTUAL_PAGE_SIZES_ARB,
GL_RGBA8, sizeof(GLint), &num_sizes);
// Get actual page sizes
glGetInternalformativ(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_X_ARB,
GL_RGBA8, sizeof(page_sizes_x),
&page_sizes_x[0]);
glGetInternalformativ(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_Y_ARB,
GL_RGBA8, sizeof(page_sizes_y),
&page_sizes_y[0]);
// Choose a page size
glTexParameteri(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_INDEX_ARB, n);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-57-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#57) 

[58 ![Sparse Textures
● Reserve and commit
● In ‗Operating System‘ terms
● Reserve – virtual allocation without physical store
● Commit – back virtual allocation with real memory
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-58-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#58) 

[59 ![Sparse Textures
● Sparse textures – commitment
● Commitment is controlled by a single function
● Uncommitted pages use no memory
● Committed pages may contain data
void glTexPageCommitmentARB(GLenum target, GLint level,
GLint xoffset, GLint yoffset,
GLint zoffset, GLsizei width,
GLsizei height, GLsizei depth,
GLboolean commit);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-59-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#59) 

[60 ![Sparse Textures
● Sparse textures – data storage
● Put data into sparse textures as normal
● glTexSubImage, glCopyTextureImage, etc.
● Use a (persistent mapped) PBO for this!
● Attach to framebuffer object + draw
● Read from sparse textures
● glReadPixels, glGetTexImage*, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-60-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#60) 

[61 ![Sparse Textures
● Sparse textures – in-shader use
● No changes to shaders
● Reads from committed regions behave normally
● Reads from uncommitted regions return junk
● Probably not junk – most likely zeros
● The spec doesn‘t mandate this, however
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-61-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#61) 

[62 ![Sparse Texture Arrays
● Combine sparse textures and arrays
● Create very long (sparse) array textures
● Some layers are resident, some are not
● Allocate new layers on demand
● New layer = glTexPageCommitmentARB
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-62-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#62) 

[63 ![Sparse Texture Arrays
● Manage your own texture memory
● Create a huge virtual array texture
● Need a new texture?
● Allocate a new layer
● Don‘t need it any more?
● Recycle or make non-resident
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-63-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#63) 

[64 ![Sparse Bindless Texture Arrays
● Use all the features!
● Create a sparse array per texture size
● As textures become needed, commit pages
● Run out of pages? Make another texture...
● Get texture bindless handles
● Use as many handles as you like
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-64-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#64) 

[65 ![Sparse Bindless Texture Arrays
● Indexing sparse bindless arrays requires:
● 64-bit texture handle
● N-bit layer index
● Remember...
● Index can diverge, handle cannot
● Need one array per-size
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-65-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#65) 

[66 ![Building Data Structures
● Okay, so how do we use these things?
● Option 1 – Build on the CPU
● It‘s just memory writes
● Use a bunch of threads
● Persistent maps
● Option 2 – Use the GPU
● Much fun. Wow.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-66-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#66) 

[67 ![Building Data Structures
● Using the GPU to set the scene (1)
● Create SSBO with AoS for draw parameters
struct DrawParams {
uint count;
uint instanceCount;
uint firstIndex;
uint baseIndex;
uint baseInstance;
};
layout (binding = 0) {
DrawParams draw_params[];
};
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-67-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#67) 

[68 ![Building Data Structures
● Using the GPU to set the scene (2)
● Create another SSBO for draw metadata
struct DrawMeta {
uint material_index;
// More per-draw meta-stuff goes here...
};
layout (binding = 0) {
DrawMeta draw_meta[];
};
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-68-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#68) 

[69 ![Building Data Structures
● Using the GPU to set the scene (3)
● Use atomic counter to append to buffers
layout (binding = 0, offset = 0) atomic_uint draw_count;
void append_draw(DrawParams params, DrawMeta meta)
{
uint index = atomicCounterIncrement(draw_count);
draw_params[index] = params;
draw_meta[index] = meta;
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-69-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#69) 

[70 ![Building Data Structures
● Using the GPU to set the scene (4)
● Dump counter, do MultiDraw*IndirectCount
glCopyBufferSubData(GL_ATOMIC_COUNTER_BUFFER,
GL_PARAMETER_BUFFER_ARB,
0, 0, sizeof(GLuint));
glMultiDrawElementsIndirectCountARB(GL_TRIANLGES,
GL_UNSIGNED_SHORT,
nullptr,
MAX_DRAWS,
0);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-70-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#70) 

[71 ![Building Data Structures
● Using the GPU to set the scene (5)
● In draw, use meta with gl_DrawIDARB
struct Material {
sampler2D tex1;
};
layout (binding = 0) uniform MaterialData {
Material material[];
};
...
oColor = texture(material[draw_meta[gl_DrawIDARB].material_index],
...);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-71-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#71) 

[72 ![John McDonald
● NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-72-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#72) 

[73 ![Putting it all into practice
● Introducing apitest
● Results
● Code review
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-73-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#73) 

[74 ![apitest
● https://github.com/nvMcJohn/apitest
● Extensible OSS Framework (Public Domain)
● Uses SDL 2.0 (Thanks SDL!)
● Initially developed by Patrick Doane
OS OpenGL D3D11
Windows Yes Yes
Linux Yes No
OSX Sorta No
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-74-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#74) 

[75 ![The Framework
● Code is segmented into Problems and
Solutions
● A Problem is a dataset to render
● A Solution is one targeted approach to
rendering that dataset (Problem)
● Support code to create shaders, load
textures, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-75-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#75) 

[76 ![The Problems So Far
● DynamicStreaming
● Render 160,000 ―particles‖ that are
dynamically generated each frame
● UntexturedObjects
● Render 643 different, untextured objects
● Different matrices per object
● No instancing allowed!
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-76-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#76) 

[77 ![The Problems So Far - Continued
● Textured Quads
● 10,000 quads using different textures
● Texture is changed between every object
● Null
● Clear and SwapBuffer
● Not going to discuss today—included as a
sanity startup.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-77-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#77) 

[78 ![Result discussion
● Results gathered on a GTX 680, using
public driver 335.23.
● But are shown normalized.
● AMD and Intel have very similar
performance ratios between solutions.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-78-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#78) 

[79 ![Decoder Ring
● SBTA = Sparse Bindless Texture Array
● SDP = Shader Draw Parameters
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-79-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#79) 

[80 ![DynamicStreaming
● Demo!
● Problem: Render 160,000 ―particles‖ that
are dynamically generated each frame
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-80-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#80) 

[81 ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-81-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#81) 

[82 ![0% 50% 100% 150% 200% 250%
GLMapPersistent
D3D11MapNoOverwrite
GLBufferSubData
D3D11UpdateSubresource
GLMapUnsynchronized
DynamicStreaming - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-82-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#82) 

[83 ![GLMapPersistent
● Map the buffer at the beginning of time
● Keep it mapped forever.
● You are responsible for safety (proper
fencing)
● Do not stomp on data in flight
● src/solutions/dynamicstreaming/gl/mappersistent.*
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-83-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#83) 

[84 ![Required Extensions
● ARB_buffer_storage
● ARB_map_buffer_range
● ARB_sync
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-84-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#84) 

[85 ![Buffer Creation
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-85-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#85) 

[86 ![Dem Flags
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-86-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#86) 

[87 ![Set circular buffer head
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-87-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#87) 

[88 ![Triple Buffering ftw
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-88-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#88) 

[89 ![Buffer Create
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-89-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#89) 

[90 ![Map me… forever.
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-90-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#90) 

[91 ![Buffer Update / Render
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-91-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#91) 

[92 ![Safety Third!
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-92-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#92) 

[93 ![Write those particles
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-93-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#93) 

[94 ![Now draw (inefficiently)
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-94-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#94) 

[95 ![Update circular buffer head
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-95-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#95) 

[96 ![UntexturedObjects
● Demo!
● Problem: Render 643 unique, untextured
objects
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-96-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#96) 

[97 ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-97-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#97) 

[98 ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-98-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#98) 

[99 ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-99-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#99) 

[100 ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-100-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#100) 

[101 ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-101-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#101) 

[102 ![GLBufferStorage-(ε|No)SDP
● Set up a giant uniform or storage buffer
with data for all objects for a frame.
● Use MDI to render many objects at once
● And PMB for dynamic data (matrix
transforms, MDI entries)
● Need a way to index data in shader (SDP)
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-102-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#102) 

[103 ![Required Extensions
● ARB_buffer_storage
● ARB_map_buffer_range
● ARB_multi_draw_indirect
● ARB_shader_draw_parameters
● ARB_shader_storage_buffer_object
● ARB_sync
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-103-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#103) 

[104 ![NoSDP
● Can be used when instancing isn‘t needed
● Very simple improvement to SDP
approach
● Not going to cover today
● So check the source code!
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-104-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#104) 

[105 ![DrawElementsIndirectCommand
struct DrawElementsIndirectCommand
{
uint count;
uint instanceCount;
uint firstIndex;
uint baseVertex;
uint baseInstance;
};
typedef DrawElementsIndirectCommand DEICmd;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-105-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#105) 

[106 ![GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_DYNAMIC_STORAGE_BIT;
mCmdHead = 0;
mCmdSize = 3 * objCount * sizeof(DEICmd);
glBindBuffer(GL_DRAW_INDIRECT_BUFFER, mCmdBuffer);
glBufferStorage(GL_DRAW_INDIRECT_BUFFER, mCmdSize, 0, createFlags);
mCmdPtr = glMapBufferRange(GL_DRAW_INDIRECT_BUFFER, 0,
mCmdSize, mapFlags);
Cmd Buffer Creation
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-106-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#106) 

[107 ![Obj Buffer Creation
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_DYNAMIC_STORAGE_BIT;
mObjHead = 0;
mObjSize = 3 * objCount * sizeof(Matrix);
glBindBuffer(GL_SHADER_STORAGE_BUFFER, mObjBuffer);
glBufferStorage(GL_SHADER_STORAGE_BUFFER, mObjSize, 0, createFlags);
mObjPtr = glMapBufferRange(GL_SHADER_STORAGE_BUFFER, 0,
mObjSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-107-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#107) 

[108 ![Cmd Buffer Update
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-108-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#108) 

[109 ![Fencing for fun and profit
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-109-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#109) 

[110 ![Someone Set Up Us The Draws
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-110-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#110) 

[111 ![Manage the Head
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-111-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#111) 

[112 ![Obj Buffer Update
// Next, update the per-Object Data
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-112-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#112) 

[113 ![Obj Buffer Update / Render
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-113-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#113) 

[114 ![Seriously though, be safe
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-114-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#114) 

[115 ![Updates to object parameters
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-115-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#115) 

[116 ![Draw all the things
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-116-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#116) 

[117 ![Head management
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-117-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#117) 

[118 ![TexturedQuads
● Demo!
● 10,000 quads using different textures
● Texture is changed between every object
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-118-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#118) 

[119 ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-119-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#119) 

[120 ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-120-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#120) 

[121 ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-121-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#121) 

[122 ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-122-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#122) 

[123 ![TexturedQuads notes
● SBTA was covered at Steam Dev Days
● Non-Sparse, Non-Bindless TextureArray is
the fallback
● Should use BufferStorage improvements
● SBTA = Sparse Bindless Texture Array
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-123-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#123) 

[124 ![GLTextureArrayMultiDraw-(ε|No)SDP
● Instead of loose textures, use arrays of Texture
Arrays
● Container contains <=2048 same-shape textures
● Shape is height, width, mipmapcount, format
● Use MDI for kickoffs
● Address is passed as {int; float} pair
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-124-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#124) 

[125 ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-125-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#125) 

[126 ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-126-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#126) 

[127 ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-127-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#127) 

[128 ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-128-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#128) 

[129 ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-129-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#129) 

[130 ![Questions?
● graham dot sellers at amd dot com
@GrahamSellers
● tim dot foley at intel dot com
@TangentVector
● cass at nvidia dot com
@casseveritt
● jmcdonald at nvidia dot com
@basisspace
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-130-320.jpg)](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/#130) 

![Approaching Zero
Driver Overhead
Cass Everitt
NVIDIA
Tim Foley
Intel
Graham Sellers
AMD
John McDonald
NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-1-320.jpg) ![Cass Everitt
● NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-2-320.jpg) ![Assertion
● OpenGL already has paths with very low
driver overhead
● You just need to know
● What they are, and
● How to use them
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-3-320.jpg) ![But first, who are we?
● Graham Sellers @GrahamSellers
● AMD OpenGL driver manager, OpenGL SuperBible author
● Tim Foley @TangentVector
● Graphics researcher, GPU language/compiler nerd
● John McDonald @basisspace
● Graphics engineer, chip architect, game developer
● Cass Everitt @casseveritt
● GL zealot, chip architect, mobile enthusiast
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-4-320.jpg) ![Many kinds of bottlenecks
● Focus here is ―driver limited‖
● App could render more, and
● GPU could render more, but
● Driver is at its limit…
● Because of expensive API calls
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-5-320.jpg) ![Some causes of driver overhead
● The CPU cost of fulfilling the
API contract
● Validation
● Hazard avoidance
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-6-320.jpg) ![Costs that add up…
● Major Categories:
● synchronization, allocation,
validation, and compilation
● Buffer updates (synchronization, allocation)
● Mapping, in-band updates
● Binding objects (validation, compilation)
● FBOs, programs, textures, buffers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-7-320.jpg) ![Remedy? – Efficient APIs!
● Buffer storage
● Texture arrays
● Multi-Draw Indirect
● Texture arrays, bindless,
sparse, indirect parameters
}Tim Foley
Graham Sellers}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-8-320.jpg) ![Results
● apitest
● Framework for testing
different ―solutions‖
● Source on github
}John McDonald
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-9-320.jpg) ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and
mostly core (GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-10-320.jpg) ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and mostly core
(GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-11-320.jpg) ![Remember, these OpenGL APIs
● Exist TODAY – already on your PC
● Are at least multi-vendor (EXT), and mostly
core (GL 4.2+)
● Coexist with existing
OpenGL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-12-320.jpg) ![On with the show…
next speaker
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-13-320.jpg) ![Tim Foley
● Intel
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-14-320.jpg) ![Challenge: More Stuff per Frame
● Varied
● Not 1000s of same instanced mesh
● Unique geometry, textures, etc.
● Dynamic
● Not just pretty skinned meshes
● Generate new geometry each frame
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-15-320.jpg) ![Want an Order of Magnitude
● Increase in unique objects per frame
● Can over-simplify as draws per frame, but
● Misses importance of variety
● Do we need a new API to achieve this?
● How far can we get with what we have today?
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-16-320.jpg) ![Three Techniques in This Talk
● Persistent-mapped buffers
● Faster streaming of dynamic geometry
● MultiDrawIndirect (MDI)
● Faster submission of many draw calls
● Packing 2D textures into arrays
● Texture changes no longer break batches
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-17-320.jpg) ![Naïve Draw Loop
foreach( object )
{
// bind framebuffer
// set depth, blending, etc. states
// bind shaders
// bind textures
// bind vertex/index buffers
WriteUniformData( object );
glDrawElements(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
0 );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-18-320.jpg) ![Typical Draw Loop
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-19-320.jpg) ![Two Ways to Improve Overhead
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
submit each batch faster
fewer, bigger batches
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-20-320.jpg) ![Pack Multiple Objects per Buffer
// sort or bucket visible objects
foreach( render target ) // framebuffer
foreach( pass ) // depth, blending, etc. states
foreach( material ) // shaders
foreach( material instance ) // textures
foreach( vertex format ) // vertex buffers
foreach( object )
{
WriteUniformData( object );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
pack multiple objects into the same
(dynamic or static) vertex/index buffer
take advantage of glDraw*() params to
index into buffer without changing
bindings
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-21-320.jpg) ![Dynamic Streaming of Geometry
● Typical dynamic vertex ring buffer
void* data = glMapBuffer(GL_ARRAY_BUFFER,
ringOffset,
dataSize,
GL_MAP_UNSYNCHRONIZED_BIT
| GL_MAP_WRITE_BIT );
WriteGeometry( data, ... );
glUnmapBuffer(GL_ARRAY_BUFFER);
ringOffset += dataSize;
// deal with wrap-around in ring, etc.
frequent mapping = overhead
no sync with GPU, but forces
sync in multi-threaded drivers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-22-320.jpg) ![BufferStorage and Persistent Map
● Allocate buffer with glBufferStorage()
● Use flags to enable persistent mapping
glBufferStorage(GL_ARRAY_BUFFER, ringSize, NULL, flags);
GLbitfield flags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
keep mapped while drawing
writes automatically visible to GPU
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-23-320.jpg) ![Dynamic Streaming of Geometry
● Map once at creation time
● No more Map/Unmap in your draw loop
● But need to do synchronization yourself
data = glMapBufferRange(ARRAY_BUFFER, 0, ringSize, flags);
WriteGeometry( data, ... );
data += dataSize;
upcoming talks will cover
glFenceSync() and glClientWaitSync()
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-24-320.jpg) ![Performance
● BufferSubData vs Map(UNSYNCHRONIZED)
● Intel: avoid frequent BufferSubData()
● NV: Map(UNSYNCH) bad for threaded drivers
● Persistent mapping best where supported
● Overhead 2-20x better than next best option
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-25-320.jpg) ![That Inner Loop Again
foreach( object )
{
WriteUniformData( object, &uniformData );
glDrawElementsBaseVertex(
GL_TRIANGLES,
object->indexCount,
GL_UNSIGNED_SHORT,
object->indexDataOffset,
object->baseVertex );
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-26-320.jpg) ![Using an Indirect Draw
DrawElementsIndirectCommand command;
foreach( object )
{
WriteUniformData( object, &uniformData );
WriteDrawCommand( object, &command );
glDrawElementsIndirect(
GL_TRIANGLES,
GL_UNSIGNED_SHORT,
&command );
}
typedef struct {
uint count;
uint instanceCount;
uint firstIndex;
uint baseVertex;
uint baseInstance;
} DrawElementsIndirectCommand;
per-object parameters are
now sourced from memory
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-27-320.jpg) ![One Multi-Draw Submits it All
DrawElementsIndirectCommand* commands = ...;
foreach( object )
{
WriteUniformData( object, &uniformData[i] );
WriteDrawCommand( object, &commands[i] );
}
glMultiDrawElementsIndirect(
GL_TRIANGLES,
GL_UNSIGNED_SHORT,
commands,
commandCount,
0 );
fill in per-object data
(use parallelism, GPU compute if you like)
kick buffered-up objects to be rendered
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-28-320.jpg) ![What if I don‘t know the count?
● Doing GPU culling, etc.
● Use ARB_indirect_parameters
● Caveat: not all HW/drivers support it
glBindBuffer( GL_DRAW_INDIRECT_BUFFER, commandBuffer );
glBindBuffer( GL_PARAMETER_BUFFER, countBuffer );
// …
glMultiDrawElementsIndirectCount(
GL_TRIANGLES, GL_UNSIGNED_SHORT,
commandOffset,
countOffset,
maxCommandCount,
0 );
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-29-320.jpg) ![Per-Draw Parameters/Data
● If shader used to take struct of uniforms
● Now take an array of such structs
● Or use SSBO to go bigger
uniform ShaderParams params;
(Shader Storage Buffer Object)
uniform ShaderParams params[MAX_BATCH_SIZE];
buffer AllTheParams { ShaderParams params[]; };
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-30-320.jpg) ![How to find your draw‘s data?
● Ideally, just index it using gl_DrawID
● Provided by ARB_shader_draw_parameters
● Not supported everywhere
● But relatively simple to implement your own
mat4 mvp = params[gl_DrawIDARB].mvp;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-31-320.jpg) ![Implement Your Own Draw ID
● Use baseInstance field of draw struct
● Increment base instance for each command
● Shader can‘t see base instance
● gl_InstanceID always counts from zero
http://www.g-truc.net/post-0518.html
cmd->baseInstance = drawCounter++;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-32-320.jpg) ![Implement Your Own Draw ID
● Use a vertex attribute
● Set as per-instance with glVertexAttribDivisor
● Fill buffer with your own IDs
● Or arbitrary other per-draw parameters
● On some HW, faster than using gl_DrawID
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-33-320.jpg) ![More MultiDrawIndirect Caveats
● If generating draws on GPU
● Use a GL buffer (obviously)
● If generating on CPU
● Intel: (Compat) faster to use ordinary host pointer
● NV: persistent-mapped buffer slightly faster
● GPU or CPU
● AMD: Array must be tightly packed for best perf
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-34-320.jpg) ![Can Be 6-10x Less Overhead
0%
100%
200%
300%
400%
500%
600%
700%
Dynamic Buffer Persistent-Mapped Multi-Draw
Normalized Objects per Second
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-35-320.jpg) ![Batching Across Texture Changes
● Bindless, sparse can help
● As you will hear
● Not all hardware supports these
● Packing 2D textures into arrays
● Works on all current hardware/drivers
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-36-320.jpg) ![Packing Textures Into Arrays
● Array groups textures with same shape
● Dimensions, format, mips, MSAA
● Texture views may allow further grouping
● Put some same-size formats together
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-37-320.jpg) ![Packing Textures Into Arrays
● Bind all arrays to pipeline at once
● Need to allocate carefully
● Based on your content requirements
● Don‘t allocate more than fits in GPU memory
uniform sampler2Darray allSamplers[MAX_ARRAY_TEXTURES];
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-38-320.jpg) ![Options for Sampler Parameters
● Pair array with different sampler objs
● Create views of array with different state
● Be careful about max texture limits
● Each combination needs a new binding slot
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-39-320.jpg) ![Accessing Packed 2D Textures
● Texture ―handle‖ is pair of indices
● Index into array of sampler2Darray
● Slice index into particular array texture
● Can store as 64 bits {int;float;}
● Or pack into 32 bits (hi/lo) no int→float convert in shader
fewer bytes to read, but more math
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-40-320.jpg) ![Texture Array ~5x Less Overhead
0%
100%
200%
300%
400%
500%
600%
glBindTexture per Object Texture Arrays No Texture
Normalized Objects per Second
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-41-320.jpg) ![Dramatically Reduced Overhead
● Possible with current GL API and HW
● Persistent-mapped buffers
● Indirect and Multi-Draws
● Packing 2D textures into arrays
● Overhead is priority for all of us on GL
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-42-320.jpg) ![Graham Sellers
● AMD
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-43-320.jpg) ![Section Overview
● Bindless textures
● Recap of traditional texture binding
● Remove texture units with bindless
● Sparse textures
● Manage virtual and physical memory
● Streaming, sparse data sets, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-44-320.jpg) ![Texture Units - Recap
● Traditional texture binding
● Create textures
● Bind to texture units
● Declare samplers in shaders
● Draw
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-45-320.jpg) ![Texture Units - Recap
● Textures bound to numbered units
● Limited number of texture units
● State changes between draws
● Driver controls residency
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-46-320.jpg) ![Texture Units - Recap
● Binding textures - API
● Very hard to coalesce draws
glGenTextures(10, &tex[0]);
glBindTexture(GL_TEXTURE_2D, tex[n]);
glTexStorage2D(GL_TEXTURE_2D, ...);
foreach (draw in draws) {
foreach (texture in draw->textures) {
glBindTexture(GL_TEXTURE_2D, tex[texture]);
}
// Other stuff
glDrawElements(...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-47-320.jpg) ![Texture Units - Recap
● Binding textures - shader
● Limited textures per shader
● All declared at global scope
layout (binding = 0) uniform sampler2D uTexture1;
layout (binding = 1) uniform sampler3D uTexture2;
out vec4 oColor;
void main(void){
oColor = texture(uTexture1, ...) +
texture(uTexture2, ...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-48-320.jpg) ![Bindless Textures
● Remove texture bindings!
● Unlimited* virtual texture bindings
● Application controls residency
● Shader accesses textures by handle
* Virtually unlimited
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-49-320.jpg) ![Bindless Textures
● Bindless textures - API
● No texture binds between draws
// Create textures as normal, get handles from textures
GLuint64 handle = glGetTextureHandleARB(tex);
// Make resident
glMakeTextureHandleResidentARB(handle);
// Communicate ‘handle’ to shader... somehow
foreach (draw) {
glDrawElements(...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-50-320.jpg) ![Bindless Textures
● Bindless textures - shader
● Shader accesses textures by handle
● Must communicate handles to shader
uniform Samplers {
sampler2D tex[500]; // Limited only by storage
};
out vec4 oColor;
void main(void) {
oColor = texture(tex[123], ...) + texture(tex[456], ...);
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-51-320.jpg) ![Bindless Textures
● Handles are 64-bit integers
● Stick them in uniform buffers
● Switch set of textures – glBindBufferRange
● Number of accessible textures limited by buffer size
● Put them in structures (AoS)
● Index with gl_DrawIDARB, gl_InstanceID
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-52-320.jpg) ![Bindless Textures – DANGER!!!
● Some caveats with bindless textures
● Divergence rules apply
● Just like indexing arrays of textures
● Bindless handle must be constant across instance
● Divergence might work
● On some implementations, it Just Works
● On others, it Just Doesn‘t
● Even when it works, it could be expensive
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-53-320.jpg) ![Sparse Textures
● Very large virtual textures
● Separate virtual and physical allocation
● Partially populated arrays, mips, cubes, etc.
● Stream data on demand
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-54-320.jpg) ![Sparse Textures
● Textures arranged as tiles
● Each tile may be resident or not
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-55-320.jpg) ![Sparse Textures
● Sparse textures – API
● That‘s it – now you have a virtual texture
// Tell OpenGL you want a sparse texture
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_SPARSE_ARB, GL_TRUE);
// Allocate storage
glTexStorage2D(GL_TEXTURE_2D, 10, GL_RGBA8, 1024, 1024);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-56-320.jpg) ![Sparse Textures
● Sparse textures – page sizes
// Query number of available page sizes
glGetInternalformativ(GL_TEXTURE_2D, GL_NUM_VIRTUAL_PAGE_SIZES_ARB,
GL_RGBA8, sizeof(GLint), &num_sizes);
// Get actual page sizes
glGetInternalformativ(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_X_ARB,
GL_RGBA8, sizeof(page_sizes_x),
&page_sizes_x[0]);
glGetInternalformativ(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_Y_ARB,
GL_RGBA8, sizeof(page_sizes_y),
&page_sizes_y[0]);
// Choose a page size
glTexParameteri(GL_TEXTURE_2D, GL_VIRTUAL_PAGE_SIZE_INDEX_ARB, n);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-57-320.jpg) ![Sparse Textures
● Reserve and commit
● In ‗Operating System‘ terms
● Reserve – virtual allocation without physical store
● Commit – back virtual allocation with real memory
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-58-320.jpg) ![Sparse Textures
● Sparse textures – commitment
● Commitment is controlled by a single function
● Uncommitted pages use no memory
● Committed pages may contain data
void glTexPageCommitmentARB(GLenum target, GLint level,
GLint xoffset, GLint yoffset,
GLint zoffset, GLsizei width,
GLsizei height, GLsizei depth,
GLboolean commit);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-59-320.jpg) ![Sparse Textures
● Sparse textures – data storage
● Put data into sparse textures as normal
● glTexSubImage, glCopyTextureImage, etc.
● Use a (persistent mapped) PBO for this!
● Attach to framebuffer object + draw
● Read from sparse textures
● glReadPixels, glGetTexImage*, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-60-320.jpg) ![Sparse Textures
● Sparse textures – in-shader use
● No changes to shaders
● Reads from committed regions behave normally
● Reads from uncommitted regions return junk
● Probably not junk – most likely zeros
● The spec doesn‘t mandate this, however
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-61-320.jpg) ![Sparse Texture Arrays
● Combine sparse textures and arrays
● Create very long (sparse) array textures
● Some layers are resident, some are not
● Allocate new layers on demand
● New layer = glTexPageCommitmentARB
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-62-320.jpg) ![Sparse Texture Arrays
● Manage your own texture memory
● Create a huge virtual array texture
● Need a new texture?
● Allocate a new layer
● Don‘t need it any more?
● Recycle or make non-resident
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-63-320.jpg) ![Sparse Bindless Texture Arrays
● Use all the features!
● Create a sparse array per texture size
● As textures become needed, commit pages
● Run out of pages? Make another texture...
● Get texture bindless handles
● Use as many handles as you like
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-64-320.jpg) ![Sparse Bindless Texture Arrays
● Indexing sparse bindless arrays requires:
● 64-bit texture handle
● N-bit layer index
● Remember...
● Index can diverge, handle cannot
● Need one array per-size
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-65-320.jpg) ![Building Data Structures
● Okay, so how do we use these things?
● Option 1 – Build on the CPU
● It‘s just memory writes
● Use a bunch of threads
● Persistent maps
● Option 2 – Use the GPU
● Much fun. Wow.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-66-320.jpg) ![Building Data Structures
● Using the GPU to set the scene (1)
● Create SSBO with AoS for draw parameters
struct DrawParams {
uint count;
uint instanceCount;
uint firstIndex;
uint baseIndex;
uint baseInstance;
};
layout (binding = 0) {
DrawParams draw_params[];
};
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-67-320.jpg) ![Building Data Structures
● Using the GPU to set the scene (2)
● Create another SSBO for draw metadata
struct DrawMeta {
uint material_index;
// More per-draw meta-stuff goes here...
};
layout (binding = 0) {
DrawMeta draw_meta[];
};
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-68-320.jpg) ![Building Data Structures
● Using the GPU to set the scene (3)
● Use atomic counter to append to buffers
layout (binding = 0, offset = 0) atomic_uint draw_count;
void append_draw(DrawParams params, DrawMeta meta)
{
uint index = atomicCounterIncrement(draw_count);
draw_params[index] = params;
draw_meta[index] = meta;
}
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-69-320.jpg) ![Building Data Structures
● Using the GPU to set the scene (4)
● Dump counter, do MultiDraw*IndirectCount
glCopyBufferSubData(GL_ATOMIC_COUNTER_BUFFER,
GL_PARAMETER_BUFFER_ARB,
0, 0, sizeof(GLuint));
glMultiDrawElementsIndirectCountARB(GL_TRIANLGES,
GL_UNSIGNED_SHORT,
nullptr,
MAX_DRAWS,
0);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-70-320.jpg) ![Building Data Structures
● Using the GPU to set the scene (5)
● In draw, use meta with gl_DrawIDARB
struct Material {
sampler2D tex1;
};
layout (binding = 0) uniform MaterialData {
Material material[];
};
...
oColor = texture(material[draw_meta[gl_DrawIDARB].material_index],
...);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-71-320.jpg) ![John McDonald
● NVIDIA
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-72-320.jpg) ![Putting it all into practice
● Introducing apitest
● Results
● Code review
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-73-320.jpg) ![apitest
● https://github.com/nvMcJohn/apitest
● Extensible OSS Framework (Public Domain)
● Uses SDL 2.0 (Thanks SDL!)
● Initially developed by Patrick Doane
OS OpenGL D3D11
Windows Yes Yes
Linux Yes No
OSX Sorta No
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-74-320.jpg) ![The Framework
● Code is segmented into Problems and
Solutions
● A Problem is a dataset to render
● A Solution is one targeted approach to
rendering that dataset (Problem)
● Support code to create shaders, load
textures, etc.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-75-320.jpg) ![The Problems So Far
● DynamicStreaming
● Render 160,000 ―particles‖ that are
dynamically generated each frame
● UntexturedObjects
● Render 643 different, untextured objects
● Different matrices per object
● No instancing allowed!
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-76-320.jpg) ![The Problems So Far - Continued
● Textured Quads
● 10,000 quads using different textures
● Texture is changed between every object
● Null
● Clear and SwapBuffer
● Not going to discuss today—included as a
sanity startup.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-77-320.jpg) ![Result discussion
● Results gathered on a GTX 680, using
public driver 335.23.
● But are shown normalized.
● AMD and Intel have very similar
performance ratios between solutions.
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-78-320.jpg) ![Decoder Ring
● SBTA = Sparse Bindless Texture Array
● SDP = Shader Draw Parameters
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-79-320.jpg) ![DynamicStreaming
● Demo!
● Problem: Render 160,000 ―particles‖ that
are dynamically generated each frame
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-80-320.jpg) ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-81-320.jpg) ![0% 50% 100% 150% 200% 250%
GLMapPersistent
D3D11MapNoOverwrite
GLBufferSubData
D3D11UpdateSubresource
GLMapUnsynchronized
DynamicStreaming - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-82-320.jpg) ![GLMapPersistent
● Map the buffer at the beginning of time
● Keep it mapped forever.
● You are responsible for safety (proper
fencing)
● Do not stomp on data in flight
● src/solutions/dynamicstreaming/gl/mappersistent.*
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-83-320.jpg) ![Required Extensions
● ARB_buffer_storage
● ARB_map_buffer_range
● ARB_sync
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-84-320.jpg) ![Buffer Creation
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-85-320.jpg) ![Dem Flags
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-86-320.jpg) ![Set circular buffer head
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-87-320.jpg) ![Triple Buffering ftw
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-88-320.jpg) ![Buffer Create
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-89-320.jpg) ![Map me… forever.
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_MAP_DYNAMIC_STORAGE_BIT;
mDestHead = 0;
mBuffSize = 3 * maxVerts * kVertexSizeBytes;
glBindBuffer(GL_ARRAY_BUFFER, mVertexBuffer);
glBufferStorage(GL_ARRAY_BUFFER, mBuffSize, nullptr, createFlags);
mVertexDataPtr = glMapBufferRange(GL_ARRAY_BUFFER, 0,
mBuffSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-90-320.jpg) ![Buffer Update / Render
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-91-320.jpg) ![Safety Third!
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-92-320.jpg) ![Write those particles
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-93-320.jpg) ![Now draw (inefficiently)
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-94-320.jpg) ![Update circular buffer head
mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes);
for (int i = 0; i < particleCount; ++i) {
const int vertexOffset = i * kVertsPerParticle;
const int thisDstOffset = mDstHead + (i * kParticleSizeBytes);
void* dst = (unsigned char*) mVertexDataPtr + thisDstOffset;
memcpy(dst, &_vertices[vertexOffset], kParticleSizeBytes);
DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle);
}
mBufferLockManager.LockRange(mDstHead, vertSizeBytes);
mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-95-320.jpg) ![UntexturedObjects
● Demo!
● Problem: Render 643 unique, untextured
objects
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-96-320.jpg) ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-97-320.jpg) ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-98-320.jpg) ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-99-320.jpg) ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-100-320.jpg) ![0% 100% 200% 300% 400% 500% 600% 700% 800% 900%
GLBufferStorage-NoSDP
GLMultiDrawBuffer-NoSDP
GLMultiDraw-NoSDP
GLBufferStorage-SDP
GLMultiDrawBuffer-SDP
GLMultiDraw-SDP
GLMapPersistent
GLDrawLoop
GLBindlessIndirect
GLTexCoord
GLUniform
D3D11Naive
GLBindless
GLDynamicBuffer
GLBufferRange
GLMapUnsynchronized
Untextured Object - Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-101-320.jpg) ![GLBufferStorage-(ε|No)SDP
● Set up a giant uniform or storage buffer
with data for all objects for a frame.
● Use MDI to render many objects at once
● And PMB for dynamic data (matrix
transforms, MDI entries)
● Need a way to index data in shader (SDP)
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-102-320.jpg) ![Required Extensions
● ARB_buffer_storage
● ARB_map_buffer_range
● ARB_multi_draw_indirect
● ARB_shader_draw_parameters
● ARB_shader_storage_buffer_object
● ARB_sync
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-103-320.jpg) ![NoSDP
● Can be used when instancing isn‘t needed
● Very simple improvement to SDP
approach
● Not going to cover today
● So check the source code!
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-104-320.jpg) ![DrawElementsIndirectCommand
struct DrawElementsIndirectCommand
{
uint count;
uint instanceCount;
uint firstIndex;
uint baseVertex;
uint baseInstance;
};
typedef DrawElementsIndirectCommand DEICmd;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-105-320.jpg) ![GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_DYNAMIC_STORAGE_BIT;
mCmdHead = 0;
mCmdSize = 3 * objCount * sizeof(DEICmd);
glBindBuffer(GL_DRAW_INDIRECT_BUFFER, mCmdBuffer);
glBufferStorage(GL_DRAW_INDIRECT_BUFFER, mCmdSize, 0, createFlags);
mCmdPtr = glMapBufferRange(GL_DRAW_INDIRECT_BUFFER, 0,
mCmdSize, mapFlags);
Cmd Buffer Creation
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-106-320.jpg) ![Obj Buffer Creation
GLbitfield mapFlags = GL_MAP_WRITE_BIT
| GL_MAP_PERSISTENT_BIT
| GL_MAP_COHERENT_BIT;
GLbitfield createFlags = mapFlags | GL_DYNAMIC_STORAGE_BIT;
mObjHead = 0;
mObjSize = 3 * objCount * sizeof(Matrix);
glBindBuffer(GL_SHADER_STORAGE_BUFFER, mObjBuffer);
glBufferStorage(GL_SHADER_STORAGE_BUFFER, mObjSize, 0, createFlags);
mObjPtr = glMapBufferRange(GL_SHADER_STORAGE_BUFFER, 0,
mObjSize, mapFlags);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-107-320.jpg) ![Cmd Buffer Update
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-108-320.jpg) ![Fencing for fun and profit
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-109-320.jpg) ![Someone Set Up Us The Draws
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-110-320.jpg) ![Manage the Head
mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) * objCount);
for (size_t u = 0; u < objCount; ++u) {
DEICmd *cmd = (mCmdPtr + mCmdHead) + u;
cmd->count = mIndexCount;
cmd->instanceCount = 1;
cmd->firstIndex = 0;
cmd->baseVertex = 0;
cmd->baseInstance = 0;
}
oldCmdHead = mCmdHead;
mCmdHead = (mCmdHead + sizeof(DEICmd) * objCount) % mCmdSize;
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-111-320.jpg) ![Obj Buffer Update
// Next, update the per-Object Data
// Next, update the per-Object Data
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-112-320.jpg) ![Obj Buffer Update / Render
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-113-320.jpg) ![Seriously though, be safe
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-114-320.jpg) ![Updates to object parameters
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-115-320.jpg) ![Draw all the things
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-116-320.jpg) ![Head management
// Next, update the per-Object Data
mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) * objCount);
for (size_t u = 0; u < objCount; ++u) {
Matrix *obj = (mObjPtr + mObjHead) + u;
(*obj) = (inObjParameters)[u];
}
glMultiDrawElementsIndirect(GL_TRIANGLES, GL_UNSIGNED_SHORT,
0, objCount, 0);
mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) * objCount);
mObjLock.LockRange(mObjHead, sizeof(Matrix) * objCount);
mObjHead = (mObjHead + sizeof(Matrix) * objCount) % mObjSize;
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-117-320.jpg) ![TexturedQuads
● Demo!
● 10,000 quads using different textures
● Texture is changed between every object
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-118-320.jpg) ![Approaching zero driver overhead](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-119-320.jpg) ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-120-320.jpg) ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-121-320.jpg) ![0% 200% 400% 600% 800% 1000% 1200% 1400% 1600% 1800% 2000%
GLSBTAMultiDraw-NoSDP
GLTextureArrayMultiDraw-NoSDP
GLBindlessMultiDraw
GLSBTAMultiDraw-SDP
GLTextureArrayMultiDraw-SDP
GLNoTex
GLTextureArray
GLNoTexUniform
GLTextureArrayUniform
GLSBTA
GLBindless
GLNaive
GLNaiveUniform
D3D11Naive
TexturedQuads – Normalized Obj/s
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-122-320.jpg) ![TexturedQuads notes
● SBTA was covered at Steam Dev Days
● Non-Sparse, Non-Bindless TextureArray is
the fallback
● Should use BufferStorage improvements
● SBTA = Sparse Bindless Texture Array
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-123-320.jpg) ![GLTextureArrayMultiDraw-(ε|No)SDP
● Instead of loose textures, use arrays of Texture
Arrays
● Container contains <=2048 same-shape textures
● Shape is height, width, mipmapcount, format
● Use MDI for kickoffs
● Address is passed as {int; float} pair
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-124-320.jpg) ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-125-320.jpg) ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-126-320.jpg) ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-127-320.jpg) ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-128-320.jpg) ![struct Tex2DAddress {
uint Container;
float Page;
};
layout (std140, binding=1) readonly buffer CB1 {
Tex2DAddress texAddress[];
};
uniform sampler2DArray TexContainer[16];
// Elsewhere (in a func, whatever)
int drawID = int(In.iDrawID);
Tex2DAddress addr = texAddress[drawID];
vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page);
vec4 texel = texture(TexContainer[addr.Container], texCoord);
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-129-320.jpg) ![Questions?
● graham dot sellers at amd dot com
@GrahamSellers
● tim dot foley at intel dot com
@TangentVector
● cass at nvidia dot com
@casseveritt
● jmcdonald at nvidia dot com
@basisspace
](https://image.slidesharecdn.com/approachingzerodriveroverhead-140320164055-phpapp01/85/Approaching-zero-driver-overhead-130-320.jpg)

- 1\. [Approaching Zero Driver Overhead Cass](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#1) Everitt NVIDIA Tim Foley Intel Graham Sellers AMD John McDonald NVIDIA
- 2\. [Cass Everitt ● NVIDIA](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#2)
- 3\. [Assertion ● OpenGL already](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#3) has paths with very low driver overhead ● You just need to know ● What they are, and ● How to use them
- 4\. [But first, who](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#4) are we? ● Graham Sellers @GrahamSellers ● AMD OpenGL driver manager, OpenGL SuperBible author ● Tim Foley @TangentVector ● Graphics researcher, GPU language/compiler nerd ● John McDonald @basisspace ● Graphics engineer, chip architect, game developer ● Cass Everitt @casseveritt ● GL zealot, chip architect, mobile enthusiast
- 5\. [Many kinds of](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#5) bottlenecks ● Focus here is ―driver limited‖ ● App could render more, and ● GPU could render more, but ● Driver is at its limit… ● Because of expensive API calls
- 6\. [Some causes of](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#6) driver overhead ● The CPU cost of fulfilling the API contract ● Validation ● Hazard avoidance
- 7\. [Costs that add](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#7) up… ● Major Categories: ● synchronization, allocation, validation, and compilation ● Buffer updates (synchronization, allocation) ● Mapping, in-band updates ● Binding objects (validation, compilation) ● FBOs, programs, textures, buffers
- 8\. [Remedy? – Efficient](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#8) APIs! ● Buffer storage ● Texture arrays ● Multi-Draw Indirect ● Texture arrays, bindless, sparse, indirect parameters }Tim Foley Graham Sellers}
- 9\. [Results ● apitest ● Framework](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#9) for testing different ―solutions‖ ● Source on github }John McDonald
- 10\. [Remember, these OpenGL](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#10) APIs ● Exist TODAY – already on your PC ● Are at least multi-vendor (EXT), and mostly core (GL 4.2+) ● Coexist with existing OpenGL
- 11\. [Remember, these OpenGL](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#11) APIs ● Exist TODAY – already on your PC ● Are at least multi-vendor (EXT), and mostly core (GL 4.2+) ● Coexist with existing OpenGL
- 12\. [Remember, these OpenGL](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#12) APIs ● Exist TODAY – already on your PC ● Are at least multi-vendor (EXT), and mostly core (GL 4.2+) ● Coexist with existing OpenGL
- 13\. [On with the](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#13) show… next speaker
- 14\. [Tim Foley ● Intel](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#14)
- 15\. [Challenge: More Stuff](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#15) per Frame ● Varied ● Not 1000s of same instanced mesh ● Unique geometry, textures, etc. ● Dynamic ● Not just pretty skinned meshes ● Generate new geometry each frame
- 16\. [Want an Order](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#16) of Magnitude ● Increase in unique objects per frame ● Can over-simplify as draws per frame, but ● Misses importance of variety ● Do we need a new API to achieve this? ● How far can we get with what we have today?
- 17\. [Three Techniques in](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#17) This Talk ● Persistent-mapped buffers ● Faster streaming of dynamic geometry ● MultiDrawIndirect (MDI) ● Faster submission of many draw calls ● Packing 2D textures into arrays ● Texture changes no longer break batches
- 18\. [Naïve Draw Loop foreach(](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#18) object ) { // bind framebuffer // set depth, blending, etc. states // bind shaders // bind textures // bind vertex/index buffers WriteUniformData( object ); glDrawElements( GL\_TRIANGLES, object->indexCount, GL\_UNSIGNED\_SHORT, 0 ); }
- 19\. [Typical Draw Loop //](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#19) sort or bucket visible objects foreach( render target ) // framebuffer foreach( pass ) // depth, blending, etc. states foreach( material ) // shaders foreach( material instance ) // textures foreach( vertex format ) // vertex buffers foreach( object ) { WriteUniformData( object ); glDrawElementsBaseVertex( GL\_TRIANGLES, object->indexCount, GL\_UNSIGNED\_SHORT, object->indexDataOffset, object->baseVertex ); }
- 20\. [Two Ways to](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#20) Improve Overhead // sort or bucket visible objects foreach( render target ) // framebuffer foreach( pass ) // depth, blending, etc. states foreach( material ) // shaders foreach( material instance ) // textures foreach( vertex format ) // vertex buffers foreach( object ) { WriteUniformData( object ); glDrawElementsBaseVertex( GL\_TRIANGLES, object->indexCount, GL\_UNSIGNED\_SHORT, object->indexDataOffset, object->baseVertex ); } submit each batch faster fewer, bigger batches
- 21\. [Pack Multiple Objects](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#21) per Buffer // sort or bucket visible objects foreach( render target ) // framebuffer foreach( pass ) // depth, blending, etc. states foreach( material ) // shaders foreach( material instance ) // textures foreach( vertex format ) // vertex buffers foreach( object ) { WriteUniformData( object ); glDrawElementsBaseVertex( GL\_TRIANGLES, object->indexCount, GL\_UNSIGNED\_SHORT, object->indexDataOffset, object->baseVertex ); } pack multiple objects into the same (dynamic or static) vertex/index buffer take advantage of glDraw\*() params to index into buffer without changing bindings
- 22\. [Dynamic Streaming of](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#22) Geometry ● Typical dynamic vertex ring buffer void\* data = glMapBuffer(GL\_ARRAY\_BUFFER, ringOffset, dataSize, GL\_MAP\_UNSYNCHRONIZED\_BIT | GL\_MAP\_WRITE\_BIT ); WriteGeometry( data,... ); glUnmapBuffer(GL\_ARRAY\_BUFFER); ringOffset += dataSize; // deal with wrap-around in ring, etc. frequent mapping = overhead no sync with GPU, but forces sync in multi-threaded drivers
- 23\. [BufferStorage and Persistent](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#23) Map ● Allocate buffer with glBufferStorage() ● Use flags to enable persistent mapping glBufferStorage(GL\_ARRAY\_BUFFER, ringSize, NULL, flags); GLbitfield flags = GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; keep mapped while drawing writes automatically visible to GPU
- 24\. [Dynamic Streaming of](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#24) Geometry ● Map once at creation time ● No more Map/Unmap in your draw loop ● But need to do synchronization yourself data = glMapBufferRange(ARRAY\_BUFFER, 0, ringSize, flags); WriteGeometry( data,... ); data += dataSize; upcoming talks will cover glFenceSync() and glClientWaitSync()
- 25\. [Performance ● BufferSubData vs](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#25) Map(UNSYNCHRONIZED) ● Intel: avoid frequent BufferSubData() ● NV: Map(UNSYNCH) bad for threaded drivers ● Persistent mapping best where supported ● Overhead 2-20x better than next best option
- 26\. [That Inner Loop](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#26) Again foreach( object ) { WriteUniformData( object, &uniformData ); glDrawElementsBaseVertex( GL\_TRIANGLES, object->indexCount, GL\_UNSIGNED\_SHORT, object->indexDataOffset, object->baseVertex ); }
- 27\. [Using an Indirect](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#27) Draw DrawElementsIndirectCommand command; foreach( object ) { WriteUniformData( object, &uniformData ); WriteDrawCommand( object, &command ); glDrawElementsIndirect( GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, &command ); } typedef struct { uint count; uint instanceCount; uint firstIndex; uint baseVertex; uint baseInstance; } DrawElementsIndirectCommand; per-object parameters are now sourced from memory
- 28\. [One Multi-Draw Submits](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#28) it All DrawElementsIndirectCommand\* commands =...; foreach( object ) { WriteUniformData( object, &uniformData\[i\] ); WriteDrawCommand( object, &commands\[i\] ); } glMultiDrawElementsIndirect( GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, commands, commandCount, 0 ); fill in per-object data (use parallelism, GPU compute if you like) kick buffered-up objects to be rendered
- 29\. [What if I](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#29) don‘t know the count? ● Doing GPU culling, etc. ● Use ARB\_indirect\_parameters ● Caveat: not all HW/drivers support it glBindBuffer( GL\_DRAW\_INDIRECT\_BUFFER, commandBuffer ); glBindBuffer( GL\_PARAMETER\_BUFFER, countBuffer ); // … glMultiDrawElementsIndirectCount( GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, commandOffset, countOffset, maxCommandCount, 0 );
- 30\. [Per-Draw Parameters/Data ● If](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#30) shader used to take struct of uniforms ● Now take an array of such structs ● Or use SSBO to go bigger uniform ShaderParams params; (Shader Storage Buffer Object) uniform ShaderParams params\[MAX\_BATCH\_SIZE\]; buffer AllTheParams { ShaderParams params\[\]; };
- 31\. [How to find](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#31) your draw‘s data? ● Ideally, just index it using gl\_DrawID ● Provided by ARB\_shader\_draw\_parameters ● Not supported everywhere ● But relatively simple to implement your own mat4 mvp = params\[gl\_DrawIDARB\].mvp;
- 32\. [Implement Your Own](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#32) Draw ID ● Use baseInstance field of draw struct ● Increment base instance for each command ● Shader can‘t see base instance ● gl\_InstanceID always counts from zero http://www.g-truc.net/post-0518.html cmd->baseInstance = drawCounter++;
- 33\. [Implement Your Own](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#33) Draw ID ● Use a vertex attribute ● Set as per-instance with glVertexAttribDivisor ● Fill buffer with your own IDs ● Or arbitrary other per-draw parameters ● On some HW, faster than using gl\_DrawID
- 34\. [More MultiDrawIndirect Caveats ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#34) If generating draws on GPU ● Use a GL buffer (obviously) ● If generating on CPU ● Intel: (Compat) faster to use ordinary host pointer ● NV: persistent-mapped buffer slightly faster ● GPU or CPU ● AMD: Array must be tightly packed for best perf
- 35\. [Can Be 6-10x](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#35) Less Overhead 0% 100% 200% 300% 400% 500% 600% 700% Dynamic Buffer Persistent-Mapped Multi-Draw Normalized Objects per Second
- 36\. [Batching Across Texture](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#36) Changes ● Bindless, sparse can help ● As you will hear ● Not all hardware supports these ● Packing 2D textures into arrays ● Works on all current hardware/drivers
- 37\. [Packing Textures Into](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#37) Arrays ● Array groups textures with same shape ● Dimensions, format, mips, MSAA ● Texture views may allow further grouping ● Put some same-size formats together
- 38\. [Packing Textures Into](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#38) Arrays ● Bind all arrays to pipeline at once ● Need to allocate carefully ● Based on your content requirements ● Don‘t allocate more than fits in GPU memory uniform sampler2Darray allSamplers\[MAX\_ARRAY\_TEXTURES\];
- 39\. [Options for Sampler](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#39) Parameters ● Pair array with different sampler objs ● Create views of array with different state ● Be careful about max texture limits ● Each combination needs a new binding slot
- 40\. [Accessing Packed 2D](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#40) Textures ● Texture ―handle‖ is pair of indices ● Index into array of sampler2Darray ● Slice index into particular array texture ● Can store as 64 bits {int;float;} ● Or pack into 32 bits (hi/lo) no int→float convert in shader fewer bytes to read, but more math
- 41\. [Texture Array ~5x](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#41) Less Overhead 0% 100% 200% 300% 400% 500% 600% glBindTexture per Object Texture Arrays No Texture Normalized Objects per Second
- 42\. [Dramatically Reduced Overhead ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#42) Possible with current GL API and HW ● Persistent-mapped buffers ● Indirect and Multi-Draws ● Packing 2D textures into arrays ● Overhead is priority for all of us on GL
- 43\. [Graham Sellers ● AMD](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#43)
- 44\. [Section Overview ● Bindless](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#44) textures ● Recap of traditional texture binding ● Remove texture units with bindless ● Sparse textures ● Manage virtual and physical memory ● Streaming, sparse data sets, etc.
- 45\. [Texture Units -](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#45) Recap ● Traditional texture binding ● Create textures ● Bind to texture units ● Declare samplers in shaders ● Draw
- 46\. [Texture Units -](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#46) Recap ● Textures bound to numbered units ● Limited number of texture units ● State changes between draws ● Driver controls residency
- 47\. [Texture Units -](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#47) Recap ● Binding textures - API ● Very hard to coalesce draws glGenTextures(10, &tex\[0\]); glBindTexture(GL\_TEXTURE\_2D, tex\[n\]); glTexStorage2D(GL\_TEXTURE\_2D,...); foreach (draw in draws) { foreach (texture in draw->textures) { glBindTexture(GL\_TEXTURE\_2D, tex\[texture\]); } // Other stuff glDrawElements(...); }
- 48\. [Texture Units -](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#48) Recap ● Binding textures - shader ● Limited textures per shader ● All declared at global scope layout (binding = 0) uniform sampler2D uTexture1; layout (binding = 1) uniform sampler3D uTexture2; out vec4 oColor; void main(void){ oColor = texture(uTexture1,...) + texture(uTexture2,...); }
- 49\. [Bindless Textures ● Remove](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#49) texture bindings! ● Unlimited\* virtual texture bindings ● Application controls residency ● Shader accesses textures by handle \* Virtually unlimited
- 50\. [Bindless Textures ● Bindless](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#50) textures - API ● No texture binds between draws // Create textures as normal, get handles from textures GLuint64 handle = glGetTextureHandleARB(tex); // Make resident glMakeTextureHandleResidentARB(handle); // Communicate ‘handle’ to shader... somehow foreach (draw) { glDrawElements(...); }
- 51\. [Bindless Textures ● Bindless](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#51) textures - shader ● Shader accesses textures by handle ● Must communicate handles to shader uniform Samplers { sampler2D tex\[500\]; // Limited only by storage }; out vec4 oColor; void main(void) { oColor = texture(tex\[123\],...) + texture(tex\[456\],...); }
- 52\. [Bindless Textures ● Handles](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#52) are 64-bit integers ● Stick them in uniform buffers ● Switch set of textures – glBindBufferRange ● Number of accessible textures limited by buffer size ● Put them in structures (AoS) ● Index with gl\_DrawIDARB, gl\_InstanceID
- 53\. [Bindless Textures –](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#53) DANGER!!! ● Some caveats with bindless textures ● Divergence rules apply ● Just like indexing arrays of textures ● Bindless handle must be constant across instance ● Divergence might work ● On some implementations, it Just Works ● On others, it Just Doesn‘t ● Even when it works, it could be expensive
- 54\. [Sparse Textures ● Very](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#54) large virtual textures ● Separate virtual and physical allocation ● Partially populated arrays, mips, cubes, etc. ● Stream data on demand
- 55\. [Sparse Textures ● Textures](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#55) arranged as tiles ● Each tile may be resident or not
- 56\. [Sparse Textures ● Sparse](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#56) textures – API ● That‘s it – now you have a virtual texture // Tell OpenGL you want a sparse texture glTexParameteri(GL\_TEXTURE\_2D, GL\_TEXTURE\_SPARSE\_ARB, GL\_TRUE); // Allocate storage glTexStorage2D(GL\_TEXTURE\_2D, 10, GL\_RGBA8, 1024, 1024);
- 57\. [Sparse Textures ● Sparse](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#57) textures – page sizes // Query number of available page sizes glGetInternalformativ(GL\_TEXTURE\_2D, GL\_NUM\_VIRTUAL\_PAGE\_SIZES\_ARB, GL\_RGBA8, sizeof(GLint), &num\_sizes); // Get actual page sizes glGetInternalformativ(GL\_TEXTURE\_2D, GL\_VIRTUAL\_PAGE\_SIZE\_X\_ARB, GL\_RGBA8, sizeof(page\_sizes\_x), &page\_sizes\_x\[0\]); glGetInternalformativ(GL\_TEXTURE\_2D, GL\_VIRTUAL\_PAGE\_SIZE\_Y\_ARB, GL\_RGBA8, sizeof(page\_sizes\_y), &page\_sizes\_y\[0\]); // Choose a page size glTexParameteri(GL\_TEXTURE\_2D, GL\_VIRTUAL\_PAGE\_SIZE\_INDEX\_ARB, n);
- 58\. [Sparse Textures ● Reserve](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#58) and commit ● In ‗Operating System‘ terms ● Reserve – virtual allocation without physical store ● Commit – back virtual allocation with real memory
- 59\. [Sparse Textures ● Sparse](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#59) textures – commitment ● Commitment is controlled by a single function ● Uncommitted pages use no memory ● Committed pages may contain data void glTexPageCommitmentARB(GLenum target, GLint level, GLint xoffset, GLint yoffset, GLint zoffset, GLsizei width, GLsizei height, GLsizei depth, GLboolean commit);
- 60\. [Sparse Textures ● Sparse](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#60) textures – data storage ● Put data into sparse textures as normal ● glTexSubImage, glCopyTextureImage, etc. ● Use a (persistent mapped) PBO for this! ● Attach to framebuffer object + draw ● Read from sparse textures ● glReadPixels, glGetTexImage\*, etc.
- 61\. [Sparse Textures ● Sparse](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#61) textures – in-shader use ● No changes to shaders ● Reads from committed regions behave normally ● Reads from uncommitted regions return junk ● Probably not junk – most likely zeros ● The spec doesn‘t mandate this, however
- 62\. [Sparse Texture Arrays ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#62) Combine sparse textures and arrays ● Create very long (sparse) array textures ● Some layers are resident, some are not ● Allocate new layers on demand ● New layer = glTexPageCommitmentARB
- 63\. [Sparse Texture Arrays ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#63) Manage your own texture memory ● Create a huge virtual array texture ● Need a new texture? ● Allocate a new layer ● Don‘t need it any more? ● Recycle or make non-resident
- 64\. [Sparse Bindless Texture](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#64) Arrays ● Use all the features! ● Create a sparse array per texture size ● As textures become needed, commit pages ● Run out of pages? Make another texture... ● Get texture bindless handles ● Use as many handles as you like
- 65\. [Sparse Bindless Texture](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#65) Arrays ● Indexing sparse bindless arrays requires: ● 64-bit texture handle ● N-bit layer index ● Remember... ● Index can diverge, handle cannot ● Need one array per-size
- 66\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#66) Okay, so how do we use these things? ● Option 1 – Build on the CPU ● It‘s just memory writes ● Use a bunch of threads ● Persistent maps ● Option 2 – Use the GPU ● Much fun. Wow.
- 67\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#67) Using the GPU to set the scene (1) ● Create SSBO with AoS for draw parameters struct DrawParams { uint count; uint instanceCount; uint firstIndex; uint baseIndex; uint baseInstance; }; layout (binding = 0) { DrawParams draw\_params\[\]; };
- 68\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#68) Using the GPU to set the scene (2) ● Create another SSBO for draw metadata struct DrawMeta { uint material\_index; // More per-draw meta-stuff goes here... }; layout (binding = 0) { DrawMeta draw\_meta\[\]; };
- 69\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#69) Using the GPU to set the scene (3) ● Use atomic counter to append to buffers layout (binding = 0, offset = 0) atomic\_uint draw\_count; void append\_draw(DrawParams params, DrawMeta meta) { uint index = atomicCounterIncrement(draw\_count); draw\_params\[index\] = params; draw\_meta\[index\] = meta; }
- 70\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#70) Using the GPU to set the scene (4) ● Dump counter, do MultiDraw\*IndirectCount glCopyBufferSubData(GL\_ATOMIC\_COUNTER\_BUFFER, GL\_PARAMETER\_BUFFER\_ARB, 0, 0, sizeof(GLuint)); glMultiDrawElementsIndirectCountARB(GL\_TRIANLGES, GL\_UNSIGNED\_SHORT, nullptr, MAX\_DRAWS, 0);
- 71\. [Building Data Structures ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#71) Using the GPU to set the scene (5) ● In draw, use meta with gl\_DrawIDARB struct Material { sampler2D tex1; }; layout (binding = 0) uniform MaterialData { Material material\[\]; };... oColor = texture(material\[draw\_meta\[gl\_DrawIDARB\].material\_index\],...);
- 72\. [John McDonald ● NVIDIA](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#72)
- 73\. [Putting it all](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#73) into practice ● Introducing apitest ● Results ● Code review
- 74\. [apitest ● https://github.com/nvMcJohn/apitest ● Extensible](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#74) OSS Framework (Public Domain) ● Uses SDL 2.0 (Thanks SDL!) ● Initially developed by Patrick Doane OS OpenGL D3D11 Windows Yes Yes Linux Yes No OSX Sorta No
- 75\. [The Framework ● Code](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#75) is segmented into Problems and Solutions ● A Problem is a dataset to render ● A Solution is one targeted approach to rendering that dataset (Problem) ● Support code to create shaders, load textures, etc.
- 76\. [The Problems So](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#76) Far ● DynamicStreaming ● Render 160,000 ―particles‖ that are dynamically generated each frame ● UntexturedObjects ● Render 643 different, untextured objects ● Different matrices per object ● No instancing allowed!
- 77\. [The Problems So](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#77) Far - Continued ● Textured Quads ● 10,000 quads using different textures ● Texture is changed between every object ● Null ● Clear and SwapBuffer ● Not going to discuss today—included as a sanity startup.
- 78\. [Result discussion ● Results](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#78) gathered on a GTX 680, using public driver 335.23. ● But are shown normalized. ● AMD and Intel have very similar performance ratios between solutions.
- 79\. [Decoder Ring ● SBTA](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#79) \= Sparse Bindless Texture Array ● SDP = Shader Draw Parameters
- 80\. [DynamicStreaming ● Demo! ● Problem:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#80) Render 160,000 ―particles‖ that are dynamically generated each frame
- 82\. [0% 50% 100%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#82) 150% 200% 250% GLMapPersistent D3D11MapNoOverwrite GLBufferSubData D3D11UpdateSubresource GLMapUnsynchronized DynamicStreaming - Normalized Obj/s
- 83\. [GLMapPersistent ● Map the](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#83) buffer at the beginning of time ● Keep it mapped forever. ● You are responsible for safety (proper fencing) ● Do not stomp on data in flight ● src/solutions/dynamicstreaming/gl/mappersistent.\*
- 84\. [Required Extensions ● ARB\_buffer\_storage ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#84) ARB\_map\_buffer\_range ● ARB\_sync
- 85\. [Buffer Creation GLbitfield mapFlags](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#85) \= GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 86\. [Dem Flags GLbitfield mapFlags](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#86) \= GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 87\. [Set circular buffer](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#87) head GLbitfield mapFlags = GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 88\. [Triple Buffering ftw GLbitfield](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#88) mapFlags = GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 89\. [Buffer Create GLbitfield mapFlags](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#89) \= GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 90\. [Map me… forever. GLbitfield](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#90) mapFlags = GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_MAP\_DYNAMIC\_STORAGE\_BIT; mDestHead = 0; mBuffSize = 3 \* maxVerts \* kVertexSizeBytes; glBindBuffer(GL\_ARRAY\_BUFFER, mVertexBuffer); glBufferStorage(GL\_ARRAY\_BUFFER, mBuffSize, nullptr, createFlags); mVertexDataPtr = glMapBufferRange(GL\_ARRAY\_BUFFER, 0, mBuffSize, mapFlags);
- 91\. [Buffer Update /](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#91) Render mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes); for (int i = 0; i < particleCount; ++i) { const int vertexOffset = i \* kVertsPerParticle; const int thisDstOffset = mDstHead + (i \* kParticleSizeBytes); void\* dst = (unsigned char\*) mVertexDataPtr + thisDstOffset; memcpy(dst, &\_vertices\[vertexOffset\], kParticleSizeBytes); DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle); } mBufferLockManager.LockRange(mDstHead, vertSizeBytes); mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
- 92\. [Safety Third! mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes); for](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#92) (int i = 0; i < particleCount; ++i) { const int vertexOffset = i \* kVertsPerParticle; const int thisDstOffset = mDstHead + (i \* kParticleSizeBytes); void\* dst = (unsigned char\*) mVertexDataPtr + thisDstOffset; memcpy(dst, &\_vertices\[vertexOffset\], kParticleSizeBytes); DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle); } mBufferLockManager.LockRange(mDstHead, vertSizeBytes); mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
- 93\. [Write those particles mBufferLockManager.WaitForLockedRange(mDstHead,](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#93) vertSizeBytes); for (int i = 0; i < particleCount; ++i) { const int vertexOffset = i \* kVertsPerParticle; const int thisDstOffset = mDstHead + (i \* kParticleSizeBytes); void\* dst = (unsigned char\*) mVertexDataPtr + thisDstOffset; memcpy(dst, &\_vertices\[vertexOffset\], kParticleSizeBytes); DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle); } mBufferLockManager.LockRange(mDstHead, vertSizeBytes); mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
- 94\. [Now draw (inefficiently) mBufferLockManager.WaitForLockedRange(mDstHead,](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#94) vertSizeBytes); for (int i = 0; i < particleCount; ++i) { const int vertexOffset = i \* kVertsPerParticle; const int thisDstOffset = mDstHead + (i \* kParticleSizeBytes); void\* dst = (unsigned char\*) mVertexDataPtr + thisDstOffset; memcpy(dst, &\_vertices\[vertexOffset\], kParticleSizeBytes); DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle); } mBufferLockManager.LockRange(mDstHead, vertSizeBytes); mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
- 95\. [Update circular buffer](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#95) head mBufferLockManager.WaitForLockedRange(mDstHead, vertSizeBytes); for (int i = 0; i < particleCount; ++i) { const int vertexOffset = i \* kVertsPerParticle; const int thisDstOffset = mDstHead + (i \* kParticleSizeBytes); void\* dst = (unsigned char\*) mVertexDataPtr + thisDstOffset; memcpy(dst, &\_vertices\[vertexOffset\], kParticleSizeBytes); DrawArrays(TRIANGLES, kStartIndex + vertexOffset, kVertsPerParticle); } mBufferLockManager.LockRange(mDstHead, vertSizeBytes); mDstHead = (mDstHead + vertSizeBytes) % mBuffSize;
- 96\. [UntexturedObjects ● Demo! ● Problem:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#96) Render 643 unique, untextured objects
- 98\. [0% 100% 200%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#98) 300% 400% 500% 600% 700% 800% 900% GLBufferStorage-NoSDP GLMultiDrawBuffer-NoSDP GLMultiDraw-NoSDP GLBufferStorage-SDP GLMultiDrawBuffer-SDP GLMultiDraw-SDP GLMapPersistent GLDrawLoop GLBindlessIndirect GLTexCoord GLUniform D3D11Naive GLBindless GLDynamicBuffer GLBufferRange GLMapUnsynchronized Untextured Object - Normalized Obj/s
- 99\. [0% 100% 200%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#99) 300% 400% 500% 600% 700% 800% 900% GLBufferStorage-NoSDP GLMultiDrawBuffer-NoSDP GLMultiDraw-NoSDP GLBufferStorage-SDP GLMultiDrawBuffer-SDP GLMultiDraw-SDP GLMapPersistent GLDrawLoop GLBindlessIndirect GLTexCoord GLUniform D3D11Naive GLBindless GLDynamicBuffer GLBufferRange GLMapUnsynchronized Untextured Object - Normalized Obj/s
- 100\. [0% 100% 200%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#100) 300% 400% 500% 600% 700% 800% 900% GLBufferStorage-NoSDP GLMultiDrawBuffer-NoSDP GLMultiDraw-NoSDP GLBufferStorage-SDP GLMultiDrawBuffer-SDP GLMultiDraw-SDP GLMapPersistent GLDrawLoop GLBindlessIndirect GLTexCoord GLUniform D3D11Naive GLBindless GLDynamicBuffer GLBufferRange GLMapUnsynchronized Untextured Object - Normalized Obj/s
- 101\. [0% 100% 200%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#101) 300% 400% 500% 600% 700% 800% 900% GLBufferStorage-NoSDP GLMultiDrawBuffer-NoSDP GLMultiDraw-NoSDP GLBufferStorage-SDP GLMultiDrawBuffer-SDP GLMultiDraw-SDP GLMapPersistent GLDrawLoop GLBindlessIndirect GLTexCoord GLUniform D3D11Naive GLBindless GLDynamicBuffer GLBufferRange GLMapUnsynchronized Untextured Object - Normalized Obj/s
- 102\. [GLBufferStorage-(ε|No)SDP ● Set up](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#102) a giant uniform or storage buffer with data for all objects for a frame. ● Use MDI to render many objects at once ● And PMB for dynamic data (matrix transforms, MDI entries) ● Need a way to index data in shader (SDP)
- 103\. [Required Extensions ● ARB\_buffer\_storage ●](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#103) ARB\_map\_buffer\_range ● ARB\_multi\_draw\_indirect ● ARB\_shader\_draw\_parameters ● ARB\_shader\_storage\_buffer\_object ● ARB\_sync
- 104\. [NoSDP ● Can be](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#104) used when instancing isn‘t needed ● Very simple improvement to SDP approach ● Not going to cover today ● So check the source code!
- 105\. [DrawElementsIndirectCommand struct DrawElementsIndirectCommand { uint count; uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#105) instanceCount; uint firstIndex; uint baseVertex; uint baseInstance; }; typedef DrawElementsIndirectCommand DEICmd;
- 106\. [GLbitfield mapFlags =](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#106) GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_DYNAMIC\_STORAGE\_BIT; mCmdHead = 0; mCmdSize = 3 \* objCount \* sizeof(DEICmd); glBindBuffer(GL\_DRAW\_INDIRECT\_BUFFER, mCmdBuffer); glBufferStorage(GL\_DRAW\_INDIRECT\_BUFFER, mCmdSize, 0, createFlags); mCmdPtr = glMapBufferRange(GL\_DRAW\_INDIRECT\_BUFFER, 0, mCmdSize, mapFlags); Cmd Buffer Creation
- 107\. [Obj Buffer Creation GLbitfield](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#107) mapFlags = GL\_MAP\_WRITE\_BIT | GL\_MAP\_PERSISTENT\_BIT | GL\_MAP\_COHERENT\_BIT; GLbitfield createFlags = mapFlags | GL\_DYNAMIC\_STORAGE\_BIT; mObjHead = 0; mObjSize = 3 \* objCount \* sizeof(Matrix); glBindBuffer(GL\_SHADER\_STORAGE\_BUFFER, mObjBuffer); glBufferStorage(GL\_SHADER\_STORAGE\_BUFFER, mObjSize, 0, createFlags); mObjPtr = glMapBufferRange(GL\_SHADER\_STORAGE\_BUFFER, 0, mObjSize, mapFlags);
- 108\. [Cmd Buffer Update mCmdLock.WaitForLockedRange(mCmdHead,](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#108) sizeof(DEICmd) \* objCount); for (size\_t u = 0; u < objCount; ++u) { DEICmd \*cmd = (mCmdPtr + mCmdHead) + u; cmd->count = mIndexCount; cmd->instanceCount = 1; cmd->firstIndex = 0; cmd->baseVertex = 0; cmd->baseInstance = 0; } oldCmdHead = mCmdHead; mCmdHead = (mCmdHead + sizeof(DEICmd) \* objCount) % mCmdSize; // Next, update the per-Object Data
- 109\. [Fencing for fun](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#109) and profit mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) \* objCount); for (size\_t u = 0; u < objCount; ++u) { DEICmd \*cmd = (mCmdPtr + mCmdHead) + u; cmd->count = mIndexCount; cmd->instanceCount = 1; cmd->firstIndex = 0; cmd->baseVertex = 0; cmd->baseInstance = 0; } oldCmdHead = mCmdHead; mCmdHead = (mCmdHead + sizeof(DEICmd) \* objCount) % mCmdSize; // Next, update the per-Object Data
- 110\. [Someone Set Up](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#110) Us The Draws mCmdLock.WaitForLockedRange(mCmdHead, sizeof(DEICmd) \* objCount); for (size\_t u = 0; u < objCount; ++u) { DEICmd \*cmd = (mCmdPtr + mCmdHead) + u; cmd->count = mIndexCount; cmd->instanceCount = 1; cmd->firstIndex = 0; cmd->baseVertex = 0; cmd->baseInstance = 0; } oldCmdHead = mCmdHead; mCmdHead = (mCmdHead + sizeof(DEICmd) \* objCount) % mCmdSize; // Next, update the per-Object Data
- 111\. [Manage the Head mCmdLock.WaitForLockedRange(mCmdHead,](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#111) sizeof(DEICmd) \* objCount); for (size\_t u = 0; u < objCount; ++u) { DEICmd \*cmd = (mCmdPtr + mCmdHead) + u; cmd->count = mIndexCount; cmd->instanceCount = 1; cmd->firstIndex = 0; cmd->baseVertex = 0; cmd->baseInstance = 0; } oldCmdHead = mCmdHead; mCmdHead = (mCmdHead + sizeof(DEICmd) \* objCount) % mCmdSize; // Next, update the per-Object Data
- 112\. [Obj Buffer Update //](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#112) Next, update the per-Object Data // Next, update the per-Object Data
- 113\. [Obj Buffer Update](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#113) / Render // Next, update the per-Object Data mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) \* objCount); for (size\_t u = 0; u < objCount; ++u) { Matrix \*obj = (mObjPtr + mObjHead) + u; (\*obj) = (inObjParameters)\[u\]; } glMultiDrawElementsIndirect(GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, 0, objCount, 0); mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) \* objCount); mObjLock.LockRange(mObjHead, sizeof(Matrix) \* objCount); mObjHead = (mObjHead + sizeof(Matrix) \* objCount) % mObjSize;
- 114\. [Seriously though, be](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#114) safe // Next, update the per-Object Data mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) \* objCount); for (size\_t u = 0; u < objCount; ++u) { Matrix \*obj = (mObjPtr + mObjHead) + u; (\*obj) = (inObjParameters)\[u\]; } glMultiDrawElementsIndirect(GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, 0, objCount, 0); mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) \* objCount); mObjLock.LockRange(mObjHead, sizeof(Matrix) \* objCount); mObjHead = (mObjHead + sizeof(Matrix) \* objCount) % mObjSize;
- 115\. [Updates to object](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#115) parameters // Next, update the per-Object Data mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) \* objCount); for (size\_t u = 0; u < objCount; ++u) { Matrix \*obj = (mObjPtr + mObjHead) + u; (\*obj) = (inObjParameters)\[u\]; } glMultiDrawElementsIndirect(GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, 0, objCount, 0); mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) \* objCount); mObjLock.LockRange(mObjHead, sizeof(Matrix) \* objCount); mObjHead = (mObjHead + sizeof(Matrix) \* objCount) % mObjSize;
- 116\. [Draw all the](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#116) things // Next, update the per-Object Data mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) \* objCount); for (size\_t u = 0; u < objCount; ++u) { Matrix \*obj = (mObjPtr + mObjHead) + u; (\*obj) = (inObjParameters)\[u\]; } glMultiDrawElementsIndirect(GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, 0, objCount, 0); mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) \* objCount); mObjLock.LockRange(mObjHead, sizeof(Matrix) \* objCount); mObjHead = (mObjHead + sizeof(Matrix) \* objCount) % mObjSize;
- 117\. [Head management // Next,](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#117) update the per-Object Data mObjLock.WaitForLockedRange(mObjHead, sizeof(Matrix) \* objCount); for (size\_t u = 0; u < objCount; ++u) { Matrix \*obj = (mObjPtr + mObjHead) + u; (\*obj) = (inObjParameters)\[u\]; } glMultiDrawElementsIndirect(GL\_TRIANGLES, GL\_UNSIGNED\_SHORT, 0, objCount, 0); mCmdLock.LockRange(oldCmdHead, sizeof(DEICmd) \* objCount); mObjLock.LockRange(mObjHead, sizeof(Matrix) \* objCount); mObjHead = (mObjHead + sizeof(Matrix) \* objCount) % mObjSize;
- 118\. [TexturedQuads ● Demo! ● 10,000](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#118) quads using different textures ● Texture is changed between every object
- 120\. [0% 200% 400%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#120) 600% 800% 1000% 1200% 1400% 1600% 1800% 2000% GLSBTAMultiDraw-NoSDP GLTextureArrayMultiDraw-NoSDP GLBindlessMultiDraw GLSBTAMultiDraw-SDP GLTextureArrayMultiDraw-SDP GLNoTex GLTextureArray GLNoTexUniform GLTextureArrayUniform GLSBTA GLBindless GLNaive GLNaiveUniform D3D11Naive TexturedQuads – Normalized Obj/s
- 121\. [0% 200% 400%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#121) 600% 800% 1000% 1200% 1400% 1600% 1800% 2000% GLSBTAMultiDraw-NoSDP GLTextureArrayMultiDraw-NoSDP GLBindlessMultiDraw GLSBTAMultiDraw-SDP GLTextureArrayMultiDraw-SDP GLNoTex GLTextureArray GLNoTexUniform GLTextureArrayUniform GLSBTA GLBindless GLNaive GLNaiveUniform D3D11Naive TexturedQuads – Normalized Obj/s
- 122\. [0% 200% 400%](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#122) 600% 800% 1000% 1200% 1400% 1600% 1800% 2000% GLSBTAMultiDraw-NoSDP GLTextureArrayMultiDraw-NoSDP GLBindlessMultiDraw GLSBTAMultiDraw-SDP GLTextureArrayMultiDraw-SDP GLNoTex GLTextureArray GLNoTexUniform GLTextureArrayUniform GLSBTA GLBindless GLNaive GLNaiveUniform D3D11Naive TexturedQuads – Normalized Obj/s
- 123\. [TexturedQuads notes ● SBTA](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#123) was covered at Steam Dev Days ● Non-Sparse, Non-Bindless TextureArray is the fallback ● Should use BufferStorage improvements ● SBTA = Sparse Bindless Texture Array
- 124\. [GLTextureArrayMultiDraw-(ε|No)SDP ● Instead of](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#124) loose textures, use arrays of Texture Arrays ● Container contains <=2048 same-shape textures ● Shape is height, width, mipmapcount, format ● Use MDI for kickoffs ● Address is passed as {int; float} pair
- 125\. [struct Tex2DAddress { uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#125) Container; float Page; }; layout (std140, binding=1) readonly buffer CB1 { Tex2DAddress texAddress\[\]; }; uniform sampler2DArray TexContainer\[16\]; // Elsewhere (in a func, whatever) int drawID = int(In.iDrawID); Tex2DAddress addr = texAddress\[drawID\]; vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page); vec4 texel = texture(TexContainer\[addr.Container\], texCoord);
- 126\. [struct Tex2DAddress { uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#126) Container; float Page; }; layout (std140, binding=1) readonly buffer CB1 { Tex2DAddress texAddress\[\]; }; uniform sampler2DArray TexContainer\[16\]; // Elsewhere (in a func, whatever) int drawID = int(In.iDrawID); Tex2DAddress addr = texAddress\[drawID\]; vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page); vec4 texel = texture(TexContainer\[addr.Container\], texCoord);
- 127\. [struct Tex2DAddress { uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#127) Container; float Page; }; layout (std140, binding=1) readonly buffer CB1 { Tex2DAddress texAddress\[\]; }; uniform sampler2DArray TexContainer\[16\]; // Elsewhere (in a func, whatever) int drawID = int(In.iDrawID); Tex2DAddress addr = texAddress\[drawID\]; vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page); vec4 texel = texture(TexContainer\[addr.Container\], texCoord);
- 128\. [struct Tex2DAddress { uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#128) Container; float Page; }; layout (std140, binding=1) readonly buffer CB1 { Tex2DAddress texAddress\[\]; }; uniform sampler2DArray TexContainer\[16\]; // Elsewhere (in a func, whatever) int drawID = int(In.iDrawID); Tex2DAddress addr = texAddress\[drawID\]; vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page); vec4 texel = texture(TexContainer\[addr.Container\], texCoord);
- 129\. [struct Tex2DAddress { uint](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#129) Container; float Page; }; layout (std140, binding=1) readonly buffer CB1 { Tex2DAddress texAddress\[\]; }; uniform sampler2DArray TexContainer\[16\]; // Elsewhere (in a func, whatever) int drawID = int(In.iDrawID); Tex2DAddress addr = texAddress\[drawID\]; vec3 texCoord = vec3(In.v2TexCoord.xy, addr.Page); vec4 texel = texture(TexContainer\[addr.Container\], texCoord);
- 130\. [Questions? ● graham dot](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#130) sellers at amd dot com @GrahamSellers ● tim dot foley at intel dot com @TangentVector ● cass at nvidia dot com @casseveritt ● jmcdonald at nvidia dot com @basisspace

### Notas del editor

- [#35:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#35)Where tightly packed == sizeof(struct) with no additional data
- [#75:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#75)\* OSX is supported, but it currently really only runs the NULL solution.
- [#77:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#77)64^3 = 262,144
- [#86:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#86)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#87:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#87)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#88:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#88)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#89:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#89)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#90:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#90)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#91:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#91)mVertexBuffer was previously gen’d into with glGenBuffers(1, &amp;mVertexBuffer);We set up for triple buffering. You can often get away with a smaller buffer (like 2x). You need to measure.Our flags are the WRITE, PERSISTENT and COHERENT bits.Then we persistently map the whole buffer.
- [#124:](https://es.slideshare.net/slideshow/approaching-zero-driver-overhead/32554457#124)BufferStorage improvements are probably worth another ~15%, bringing the total speedup to ~22x over D3D11.