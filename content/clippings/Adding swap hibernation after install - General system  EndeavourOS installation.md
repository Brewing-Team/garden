---
title: "Adding swap /hibernation after install - General system / EndeavourOS installation"
source: "https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/27?u=flyingcakes"
author:
  - "[[EndeavourOS]]"
published: 2020-12-30
created: 2025-10-09
description: "I did a fresh install again on a new laptop dual boot Windows. I created a partition for linux and used replace partition in the installer. Ive been messing with this trying to figure out the best setup. I want the syste…"
tags:
  - "clippings"
---
## Adding swap /hibernation after install

[General system](https://forum.endeavouros.com/c/general-system/5) [EndeavourOS installation](https://forum.endeavouros.com/c/general-system/endeavouros-installation/64)

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/otherbarry/96/10801_2.png)](https://forum.endeavouros.com/u/otherbarry)

[otherbarry](https://forum.endeavouros.com/u/otherbarry)

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/26 "Post date")

That is my point though, copy and paste is not really learning.

It is the old teach someone to fish rather than catching fish for them conundrum.

Users can still create threads with the WHY questions, nobody is suggesting the Arch Wiki should be used in solitary isolation. Better quality help can be given in this way than by giving them a copy and paste solution that is not understood.

Anyway, each to their own. Like I said we are all trying to help, just in our own ways.

Take notes. I have a terrible memory and rely on the detailed notes I have taken over the years.

I use Cherrytree for this, but you can you whatever note taking app you prefer.

It is a good habit to get into.

This is also why learning concepts is more important than commands, they are easier to remember.

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/tlmiller76/96/96350_2.png)](https://forum.endeavouros.com/u/tlmiller76)

[tlmiller76](https://forum.endeavouros.com/u/tlmiller76)

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/27 "Post date")

I’ll admit with stuff like this, I’ve never remembered a single thing. I still have to google “swap fstab entry” EVERY TIME I set up a swap file to get the “none swap defaults” portion right.

But I figure since we all pretty much carry a computer with us 24/7, as long as I remember that I need to do the thing, google can find how to do the thing properly for me.

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/joekamprad/96/77608_2.png)](https://forum.endeavouros.com/u/joekamprad)

[joekamprad](https://forum.endeavouros.com/u/joekamprad) Der Doktor

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/28 "Post date")

> command line parameter “resume\_offset=” allowing us to specify  
> the offset, in <PAGE\_SIZE> units, from the beginning of the partition pointed  
> to by the “resume=” parameter at which the swap header is located.

Source: [https://www.lkml.org/lkml/2006/9/23/41](https://www.lkml.org/lkml/2006/9/23/41)

I do not find any information if this is needed or optional? But looks like needed for hibernating to get the info on where to find the swapfile?

The swapfile implementation on calamares seems to not create **resume\_offset=** entry on swapfile installs… but it also do not have the same selection as for swap partition where you can choose “swap with hibernate”

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/joekamprad/96/77608_2.png)](https://forum.endeavouros.com/u/joekamprad)

[joekamprad](https://forum.endeavouros.com/u/joekamprad) Der Doktor

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/29 "Post date")

*Feel free to discuss such thing: open another post to do so.*

As it is not helping the topic to get solved  
You could give info instead or link to the parts of the Archwiki and give background info on what it provides.

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/pebcak/96/100472_2.png)](https://forum.endeavouros.com/u/pebcak)

[pebcak](https://forum.endeavouros.com/u/pebcak)

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/30 "Post date")

`resume=UUID` points to the device/volume which harbors the swapfile  
`resume_offset` points to where on that device the file is to be found

??

[![](https://forum.endeavouros.com/user_avatar/forum.endeavouros.com/bonk/96/112014_2.png)](https://forum.endeavouros.com/u/bonk)

[BONK](https://forum.endeavouros.com/u/bonk)

[Dec 2020](https://forum.endeavouros.com/t/adding-swap-hibernation-after-install/10831/31 "Post date")

The arch wiki is a convoluted masterpiece of an oxymoron. I always wonder what the attraction is to figuring out how to set up your os is more fun and takes up more of your time then actually using it. Yes this is a serious forum but I think we try to have fun as well. It should not feel like work supporting the forum. If [@joekamprad](https://forum.endeavouros.com/u/joekamprad) or anyone else wants to provide help as they see fit it is their prerogative.