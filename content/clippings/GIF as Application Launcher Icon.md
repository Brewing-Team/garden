---
title: "GIF as Application Launcher Icon"
source: "https://www.reddit.com/r/kde/comments/85g4yx/gif_as_application_launcher_icon/"
author:
  - "[[[deleted]]]"
published: 2018-03-19
created: 2025-10-26
description:
tags:
  - "clippings"
---
Is it possible to import a GIF as the image icon for Application Launcher? Any alternatives to Application Launcher that might support this format?

---

## Comments

> **Zren** • [11 points](https://reddit.com/r/kde/comments/85g4yx/comment/dvx9vkm/) •
> 
> QML's [Image](http://doc.qt.io/qt-5/qml-qtquick-image.html)/icons don't animate by default. Plasma uses it's own [PlasmaCore.IconItem](https://api.kde.org/frameworks/plasma-framework/html/classIconItem.html) which simplifies loading the icons/images, but also doesn't support animated gifs. You'll need to change it to [AnimatedImage](http://doc.qt.io/qt-5/qml-qtquick-animatedimage.html).
> 
> In `/usr/share/plasma/plasmoids/org.kde.plasma.kickoff/contents/ui/Kickoff.qml` there's a `PlasmaCore.IconItem` which draws the panel icon.
> 
>     PlasmaCore.IconItem {
>         anchors.fill: parent
>         source: plasmoid.icon
>         active: parent.containsMouse || compactDragArea.containsDrag
>         smooth: true
>     }
> 
> which you'll want to change to
> 
>     AnimatedImage {
>         anchors.fill: parent
>         source: "/home/chris/Pictures/Wallpapers/GifWallpaper/Meh/giphy-CHYAgciQkgKPK.gif"
>         smooth: true
>     }
> 
> Then you'll want to restart plasmashell with:
> 
> killall plasmashell; kstart5 plasmashell
> 
> Example: [https://streamable.com/t7980](https://streamable.com/t7980)
> 
> Note that while modifying `/usr/share/plasma/...` will work, Plasma updates may override your changes. We could copy the widget and rename it something else, but you'd effectively be freezing the code and wouldn't get bugfixes/new features.
> 
> > **\[deleted\]** • [3 points](https://reddit.com/r/kde/comments/85g4yx/comment/dvxiwwj/) •
> > 
> > I wonder how hard it would be to make a separate widget out of this as a sort of alternative?
> > 
> > > **Zren** • [2 points](https://reddit.com/r/kde/comments/85g4yx/comment/dvyfguw/) •
> > > 
> > > Huh, that might actually be possible to do. All we to do is "extend" the `Kickoff.qml` file and override the `Plasmoid.compactRepresentation` property.
> > > 
> > > First the expanation, then the example at the bottom.
> > > 
> > > Edit: Woops, forgot to delete something so this doesn't actually work. Give me an hour or two to fix this.
> 
> **\[deleted\]** • [2 points](https://reddit.com/r/kde/comments/85g4yx/comment/dvxkegy/) •
> 
> Appreciate the response, Zren. I'll have to play around with this.