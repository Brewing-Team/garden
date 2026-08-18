---
title: "Kenny Chinn - Moving Renderer to a thread"
source: "https://www.kenny-chinn.com/chronicle-engine/moving-renderer-to-a-thread"
author:
published:
created: 2026-08-10
description: "Threaded RendererIt's been a long time since I've posted, and honestly since I've had the time to really do much work on Chronicle. Now that I've found some time again, I decided it was time to work on the performance of the renderer some. So I decided to move rendering to it's own thread to help"
tags:
  - "clippings"
---
### Threaded Renderer

It's been a long time since I've posted, and honestly since I've had the time to really do much work on Chronicle. Now that I've found some time again, I decided it was time to work on the performance of the renderer some. So I decided to move rendering to it's own thread to help with performance in large scenes that tended to get get bogged down by waiting on the rendering work to complete. After complete this work Chronicle can now hit 40-50 fps in a scene with 1000 animating characters.

### Render Messages

The first step to this work is removing any direct references between objects/components and the renderer. As an example before this work the MeshComponent was directly creating/managing the renderable instance for the mesh itself, and the renderer would do things like collect all active light components during it's update to process lights. It's easy to see how this design isn't great in general but even more so if the renderer is running in a completely separate thread at all times.

After refreshing myself on how everything was interacting with and by the renderer I came up with these messages to maintain current functionality in this new paradigm.

- RenderSetDeltaTimeCommand - Forwards the delta time that was used to generate commands for this frame
- CreateRenderableCommand - This command created a renderable instance with the provided setup
	- Non-rendering code now references renderables via an ID that is provided with any message used to update it
- UpdateRenderableCommand - Updates target renderable's transform
- UpdateRenderableBonesCommand - Update bone transforms on target renderable
- DestroyRenderableCommand - Destroy target renderable
- DrawDebugRenderableCommand
- DrawDebugLineCommand
- DestoryDebugLinesCommand - Debug lines are the only debug renderable that can persist more than a frame
- PushImguiDrawDataCommand - This command copies the imgui draw commands so that they can be displayed later
- CreateLightCommand
- EnableLightCommand
- UpdateLightCommand
- DestroyLightCommand
- CreateBillboardCommand
- UpdateBillboardCommand
- DestroyBillboardCommand

So 16 messages to maintain current functionality isn't too bad, even if the Chronicle renderer is pretty simple. Now that we know what message we need, how do we send and receive these messages? Luckily Chronicle already has a messaging system used by the object and component system! It's talked about some in this [post](https://www.kenny-chinn.com/chronicle-engine/objects#h.glvn5sg9jbce), but the quick overview is CrMessageDispatcher handles registering callbacks for specific messages, and queuing and processing any messages sent to the dispatcher. In Chronicle every CrObject has it's own dispatcher used for sending messages between components on the same object, and there is also a GlobalMessageDispatcher(just a CrMessageDispatcher that lives on the WorldManager) that can be used for sending messages between objects. The object and global message dispatchers work by queuing up any messages sent to them, and then during each update stage all queued messages are processed before the object's components update(or worlds in the globals case). The renderer won't have multiple update stages, and it needs to keep all messages from one frame together, so the use case is slightly different. The quick solution is to give the renderer a looping array of MessageDispatchers and maintain a read and write index into it.

The number of dispatches can be configured via an init file(minimum of 3). The read index is updated by the renderer after it's processed messages in the current read dispatcher, if the renderer somehow catches up with the CPU side it will just re-use the same read index essentially processing 0 messages next update, but it's not a common case. The write index is updated at the start of the CPU side update, if the new write index would be the same as the read index the CPU will wait until the renderer has updated the read index. So it's still possible to stall waiting on the renderer, but it's not as common as it was before.

### Renderable Instances to Renderable Ids

As mentioned above to support this work components like the MeshComponent needed to be changes from directly manipulating render instances to instead sending messages with an ID instead. Before there was public functions to Create/Destory renderable instances anything could call, and the create just returned a raw ptr to the created instance. Now those functions are gone, even though the RenderableInstances still exist on the renderer side, but are hidden from the rest of the engine behind IDs. To replace those functions there is now a manager that IDs can be requested from. So the new flow for the mesh component is Request a render ID, then send a CreateRenderableCommand with the ID, the mesh resource, starting transform, if it casts shadows, and if back faces should be rendered.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQUxOFTNOTBAVrOrwx7ZPPxtu4LNgdb9Fn6JwRWBVLXZP7x8PCtVoukshTxDsSLXvR0JM0OGqQDAcsdhCzj2TRSU6lkePgC7CcNO11ms5WHb5eyeYpVAaRStk1VIx382GdcomzN4Uxc3D-TPvd2Rpm0W0-OhF6lNIch38Y8Za5J7diOQT21KWbFCjScObPun924E04VgSq8cF_WIQ-V0yRjVzXoQ_rAYNdZLuhQER7Q=w1280)

Lights and billboards have a similar treatment with IDs requestable on CPU side, and actual creation and manipulation all done via these new messages.

### Thread pool updates

A quick overview of chronicle's thread pool can be found [here](https://www.kenny-chinn.com/chronicle-engine/resource-manager#h.kxn51b5xepbg). The main change to the pool was adding a new Render task type so that on engine init a renderer task(that never finishes) can be created and picked up the designated render thread.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQXsj1TgZLOx2mbTSfh8icxh9It81MhRjlgWeO4VlNUiO62Pvwl8kpSitEvu6x6MXwGKNVG_epAFY6sWaYdtahuawZM_fYcY9pokr7AKNPCzs7JmnsVJmCcWy82t8RnVLraYJ2sTchHHQoxt1Wgs7w1Bn_Vfnz2FDugT4ELDm78juzgFqd32q2vtSQUOgeSdj0SgIWVC3Fyh7Ok9mW5d21f_lOC-doImo93iQSu3Udk=w1280)

Then creating the threaded render task during engine init looks like this.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQWbpTvDWk31VHMOt0hZ2QeeERvJG_afh8WfP3evaAwXUlV7XJXpoczy5Vj8qBnoJkFW8VjrR625Goqz38fT-RYpyolgwqBFOfVtDcB3LiZdr5jt0okm0Wr6YGaS3KNaBRsykxCKpS4Cdl8k_M6yPCULY1Mh2Jn5LiNzduGT0rk4iTOq7uSeA9AyU8qKogfKkd65Gj_Wx5x-w4WfXuTS-x_wwBYflL7_hfKaPZqy=w1280)

### Other Improvements

Another thing that was missing from my awful renderer was any sort of frustum culling, so even if a mesh was completely behind the camera it was still getting sent to GPU for no reason. So during this threading work I added a simple visibility test that just does a dot product between the camera forward vector and the vector from the camera to the center and each corner of a meshes bounding box to check if it's at least in front of the camera.

### Issues

While this is all working there are a few issues still to work out. The biggest one is probably the imgui integration with all of this, by duplicating the draw commands output from imgui and drawing them later I've introduced some flickering into the imgui overlay that I need to track down. It's distracting but usable haha. The other issue is this didn't mesh well with my tools done in QT, I think because QT has it's own threading model and is causing the engine to get pumped slightly different led to some deadlocks in the world editor. Luckily it was pretty simple to go the old route only editor and run the renderer on the main thread like before, just wrapped the task creation in a pragma, and had the tools engine update loop work like it did before and directly tick the renderer.

### Demo video

Short video showing chronicle running with 1000 animated characters in the scene. This post was brief, but I hope to make more in-depth posts soon focused on animation systems.

![](https://www.youtube.com/watch?v=K2RCqFSfy8I)

Página actualizada

Denunciar abuso

Este sitio web emplea cookies de Google para ofrecer sus servicios y analizar el tráfico. La información sobre tu uso de este sitio web se comparte con Google. Al utilizar el sitio web, aceptas el uso de cookies.

[Más información](https://www.google.com/policies/technologies/cookies/)

Entendido