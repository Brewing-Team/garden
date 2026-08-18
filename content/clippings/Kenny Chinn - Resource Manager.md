---
title: Kenny Chinn - Resource Manager
source: https://www.kenny-chinn.com/chronicle-engine/resource-manager
author:
published:
created: 2026-08-10
description: "Resource ManagementAn important component of any game engine is resource management, including: meshes, textures, animations, sounds, and any other type of data your game needs to read off disk. You should only load what you need, for as long as it's needed, so it's important to include a way to"
tags:
  - clippings
  - resource-managent
---
### Resource Management

An important component of any game engine is resource management, including: meshes, textures, animations, sounds, and any other type of data your game needs to read off disk. You should only load what you need, for as long as it's needed, so it's important to include a way to track what resources are still in use and free them up when they are no longer needed. It's also important to make sure loading a resource won't cause performance issues. Since file IO is one of the slowest things you can do on a computer these days, any game engine resource manager needs the option to be asynchronous (blocking loads are still needed in some cases) so the slow IO can be done in the background.

The first resource manager for Chronicle was only blocking, so a file load could cause a noticeable performance drop. This was fine when all I had were small test worlds with relatively few assets in them and that didn't require intense file loading. However, as the engine / tools have grown and I've created bigger worlds using more varied assets, this approach became a bottleneck every time I loaded a world to test a new feature. It was time to refactor how Chronicle's resource management worked!

Here's an overview of how it currently works, including the base resource class, resource handles, thread pool, and manager.

### ResourceBase

The screenshot above shows the base class from which all resources derive. It's main purpose is to track the state of the resource: empty, loading, ready, or failed. There are other options that don't require using inheritance to achieve this, but this is the most straight forward and makes it easier for another engineer to easily see what is required of any new resource type they add. The macro at the top is a convenient way to add some helpful static functions to all resource types for getting both the type name and a hash of said type name.

All resource types need to implement Reload and Load methods. Load is for loading a fresh resource from disk, while Reload is for updating an already loaded resource from its file on disk. Reload is used in a few places in the tools so that edits to, for instance, a mesh get picked up as soon as the file changes and updates the render of the mesh.

The only thing that actually updates the state of a resource is the ResourceManager, hence the use of friend here. The resource stores its state, but doesn't control it since the manager is what controls the state and when it can update.

Below, you can see a simple example of a resource type. My last post about AudioClipResource detailed adding audio to Chronicle. You see that declare macro being used with Load / Reload being implemented. The last part of adding a new resource type is registering it with the ResourceManager on startup which I will cover a bit later.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQXXtNm-VzlTnitmr4yzp-biF36h3wCR14_cfVnPZATkyHe0_9-hkgDRVVpJPAyTcFMWTqcVf9hoaFltWgg64oB9VIUgdM8aXP19gTu8BBBYOrxxoCDooG8wMtFhefXzBinQeL2XCMfW2IUzP-aRYPgyck96j6irqb8HqdcAVER9XwpUfV8Ercs7m5kftOCU7IUnpx3J_owp2KB5_FUQyPTj4qXeIi2FK9CIbYy3VKE=w1280) ![](https://lh3.googleusercontent.com/sitesv/AG8ngQWaLVZ6nNmQd5TwfuOa0fPmZdmf7ncRnhaPJWCxJiAnHhlQ_wEy98BM6xNCbt-nAIhUaDh9_EVtw4QnqSJTXYpkRszVwuuKxGLiY62-tDBmNbW8cWXvtRlktVlo3C10GjqHMtISBi1-qv0hVxH6_NUqJtQlzRbLJax98lB6lckJ4EmMQiFFoZAUqWujucL3fFNcY6b25dwpZ5DoVAII811_HRj_kPOp16vUHPZhSAQ=w1280)

### ResourceHandle

Next up is the ResourceHandle. This is a wrapper around a shared pointer of the actual resource instance. It's better to create this wrapper layer instead of just using / passing shared pointers to the resource because it more easily handles tracking when a resource is no longer being referenced. It also gives you a good place to write utility functions for checking if a resource is ready to use without needing to write nullptr checks; then, IsReady checks all over game code.

Why is this easier for tracking when a resource is unused? Because the ResourceHandleBase destructor can check the reference count on the shared pointer, and if this handle holds the last reference to it, then the handle can notify the resource manager that the resource is now unused. The resource doesn't get unloaded right away, but is instead flagged as unused, so if something else later in the frame does get a reference to the resource, it will just be removed from the unused list. Without this, the resource manager would instead periodically need to check how many references still exist to any loaded resources which can be costly if the amount of loaded resources gets large.

The templated ResourceHandle is there to make it explicit what resource a system is expecting, and it handles all of the casting from ResourceBase since that's the type of the shared pointers the ResourceManager hangs onto.

### Thread Pool

Since this is an asynchronous resource manager, I do want to explore how Chronicle's thread pool works. For a good look at a basic thread pool, visit [https://github.com/vit-vit/CTPL](https://www.google.com/url?q=https%3A%2F%2Fgithub.com%2Fvit-vit%2FCTPL&sa=D&sntz=1&usg=AOvVaw0KbotamqRe-uSQKn74U1VI). The Chronicle thread pool is similar, but instead of having a single queue of tasks, it has multiple queues for different types of tasks. Example tasks types include: General, FileIO, and Animation. The thread pools initialize parameters and specify how many threads each task type can use, then each thread is created as either a specific task type it should run or a general. If a thread is set to run FileIO commands, it will always begin by checking the FileIO queue and run those tasks first, but if the FileIO queue is empty, it will then check the General queue and run those tasks. A FileIO thread won't run any other type of tasks. This makes it so you can have threads that prioritize FileIO work, but if there is no FileIO work to do (and most of the time, there isn't), those threads won't be idle and can pick General tasks as well. When a task is created / pushed to the thread pool, it can specify it's type so it gets added to the corresponding queue or the General queue.

Below is a Tracy image showing two threads doing a bunch of AsyncLoad tasks, which are reading a file off disk then calling the resource->Load() to load a resource. Some of those tasks run across frame boundaries, and once there's no FileIO work to do, those two threads start picking up General tasks, in this case object/component updates.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQW81MueqIR47Qf8DxI5_xwBX6qQH1ITdIEjOVauL6Y06q12eeSgvXDxxGJaElG0JllEqUWP1Y72DtlvPaY69PIAN9PE5LBQBFu64iLsOyArkgDOCr2gNX_rx7GKPSnz4DZUYWBJpy_hnQmzvZoeiQWS4DO7dxhO5ItkKoCda23XTG749nDOt0rDfruImr5KkT7w3MPXB_KGVucqBmZoQz1gKI5kPSRhthvN2oCQ=w1280)

### Resource Manager

Now that we've covered all the required prerequisites we can talk about the actual resource manager. The ResourceManager is first a factory for ResourceTypes that have been registered with it. So the first image below is the ResourceMaker and it's interface. It's a pretty classic C++ factory setup, a base interface/class that the factory can hold onto with a derived templated class to override the required functions to create the specific type of object. One thing that might stand out is this maker has a LoadResource and CreateResourcePtr methods, instead of just a LoadResource. The manager will create a resource as soon as it's requested so that it has a place valid object to update state for(Ready, Failed, Loading). It also means it can store the pointer in it's maps and return handles for any requests later in the frame for the same resource. The LoadResource is what is eventually called in the AsyncLoad when the file has been read in. It might seem a bit wasteful to create the resource upfront when it could be quite a while before it's ready, but since I decided to store the resource state in the base resource class it's required, and with the handles wrapping the resource pointers there are protections in place to keep users from accessing these resource pointers that aren't really resources yet.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQX1UHmRIScQNvPz_0dDk2PzGo1xxx0oBndh0WxDECISSHVQ9pX-nTIeFtpqjjrtiEB309gMx_ggSmOpa7olPLcf1-FQAiSoLOkgiS4YGsBN3ohLv0XrFheyePR-7CMf3ZHssBFHp9V6UxdKqUJuBX3R5ZpVIm_GRv7NgYUf0KCQKUDO1-WguQmQsokk-j8DsI_ROMSvUI8wuwe33X6KZKsP79gNdnL6N3DQ0dv0PZ4=w1280) ![](https://lh3.googleusercontent.com/sitesv/AG8ngQV-dxR3XoXJYEnfk6wmpAzcoOwQmUfv1klHsGN_WMXMrMSfMDwyLvtmXMw3S2GXaOPLp_j8K3tGfiimWIrfRfSHinbsWFannBXwS-qNxoyiljx5XTZ-nNziItfcr-4pS7_RgbbMrB8BX5QX1X6oNJVXivzbeA7fPeAVBJKIrf_dbaylKG8MftTyEWOjwZQaCZ01GbnjWjx9bR4Tbc31erH5zvHt2enfv5DNtAhJ=w1280)

Above this you can see a quick example of a resource type being registered with the ResourceManager. I should probably change the register to be a templated function that creates the static ResourceMaker instead of having the user handle that part as it is now, but for now it gets the job done. The file extension is provided as part of the makers constructor so that the resource manager can verify filenames that are requested as well as load a resource correctly with the more generic non-templated load function.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQVB9tl0cgUkLAt_IX91wUOahBwyok-atFCPGqONJ4Z9AiTr1enK__Z7XDoisNHg7_MiANhhEWn3nU98HglSF5LNETt0VzXIjqp-Xtl-ZUF_KrqGrNvXgh_VPxVCOkh3uwAzdfot2N28wLAALmtmU185Y1WId-LXf2jvtaC7uDJZ5m8O0z_Jk8QFFV0q-ZyVZdeGBCkCAQ-JlBbD2UnbdY2yh6eoWljqeF65RTq9=w1280)

Above is the ResourceManager class. It's a singleton and I use the static Instance, Destroy methods to control the lifetime of it as seen for other singletons in Chronicle such as the AudioEngine. Currently resources are all manged via filepaths, long term I need to convert this to unique resource Ids such as GUIDs or filepath hashes, but that will require more work on the tools and pipeline side of things than the runtime.

Functions of note:

- LoadResource
	- Templated - Tries to load the provided filepath as a ResourceType, will validate the extension from the registered maker against the filepath.
		- Non-templated - Tries to load the provided filepath, the ResourceType is resolved from registered extensions.
- GetResource - Will look up the provided filepath in already loaded/requested resources and return a handle to it. If it's not loaded it will return an empty handle.
- UpdatePendingLoads - This function is meant to be called every frame. It checks for any finished load requests, and completed requests get there state updated to ready/failed depending on the results. This happens in the main thread as you don't want the state of a resource to change mid frame let alone half way through an object update on another thread.
- ReloadResource - Used to request a loaded resource be loaded from disk again.
- GetResourceTypesAndExtensions - This tools only method is used by the Resource Browser widget to auto populate all registered resource types.
- UnloadUnusedResources - This function is meant to be called once every X frames. This goes through the mUnusedList and frees up any resources that still have no external references.
- AddResourceToUnusedList - This private function is actually called by the ResourceHandle destructor if the pointer reference count becomes 2(ResourceManager has 1 reference, and the destructing handle still has 1).

As far as the member variables go, as you can see it leverages several maps for quick look up of resources via filepath, as well as reverse maps of pointer to filepath. Then a few vectors for queuing up finished, failed, and unused resources that get resolved in the main/single threaded functions. And of course a couple of mutexes to make sure maps/vectors aren't being written/read to/from multiple threads at once.

![](https://lh3.googleusercontent.com/sitesv/AG8ngQWhECZhhTHRraq0rH982673mr067BCIFJLnOtBWPYh9xGGhR20pNyr2X4dSonAWFkCLUKWdN0HydLxJ7IZZDvKdbVQsm4mDBF9QWyzBmW9zdlT1KPt8LeZsEWwYa5q6jj7V_49x3_d0Dmd3C2Fdx7xhdiwqDOZByMxB9HvIxhUqzDoiXb_kiwHoEDK89W_qzr-C6Y-oYRpwZgjZfmDu0kmIGsOp0p8aHxEQKuVk=w1280)

Above is the meat of the LoadResource function. Above this is the checks to see if the resource is already requested/loaded, and validating the extension and ResourceType. First thing we do if this is a new resource is create the shared pointer for the resource, then release the lock on the map. It's important to release the lock here since we're done updating the map, and there is always a chance a resource load method could make more load requests and you end up in a dead lock if the lock is held onto any longer. Next, if the load is marked as blocking the LoadResource on the maker is called immediately, which also does the FileIO. If it's not blocking the loadTask lambda is created and pushed into the ThreadPool. Inside the lambda you'll see it just calls LoadResource like a blocking load, but then based on the result the resource gets added to finished/failed vector which will be processed the next frame as part UpdatePendingLoads and the resources state will be updated from loading to ready/failed.

The biggest hurdle when refactoring the resource manager to be asynchronous was updating all the places using the blocking loads to handle not having the requested resources on request, but instead maybe having to wait a few frames to be ready. This mostly came up in components that used resources, before this a lot of them loaded resources in OnAddToWorld, and then just used them in there Update functions. Now it's not guaranteed a resource will be ready for the components first update, so these components had to be updated to check the resource handles for IsReady, and if the component need to do some work based on the loaded resource it had to be handled once it's required resources were ready. One side note is that currently all the tools do blocking loads, since it doesn't make much sense for a tool to show/do anything until all the data is there for editing, and also the tools are all in Qt which has it's own environment that can be a little more unpredictable than the runtime game loop.

Currently Chronicle has nine resource types that are handled via the ResourceManager.

1. AnimClipResource
2. AnimRig
3. AnimSet
4. AnimationBlendGraph
5. AnimationStateMachine
6. AudioClipResource
7. PhysicsMeshResource
8. MeshResource
9. TextureResource

You'll notice Worlds, and Objects are not in that list. For now worlds and objects loaded outside the resource manager as blocking loads. This is mainly due to how the lifetimes of worlds and objects are handled as well as how the reflection loading works. It should be possible to update the world and objects to be part of the ResourceManager, but for now I've kept them separate as the ResourceManager was ironed out for the other use cases.

![](https://www.youtube.com/watch?v=dXZKv3GknWI)

The above video is showing the debug info about the number of loaded resources as worlds are loaded and unloaded. The biggest visual give away that resources are loaded asynchronously is you can see textures pop in after the meshes over a few frames. This happens because currently materials are what contain references to textures and materials are baked into the MeshResource, so the textures won't be requested until the mesh is loading/loaded. You'll notice the counts don't drop instantly, and that's because the unused list is only processed once every so many frames. This helps catch resources getting reused before they are unloaded as well not doing work to unload resources every frame.

Página actualizada

Denunciar abuso