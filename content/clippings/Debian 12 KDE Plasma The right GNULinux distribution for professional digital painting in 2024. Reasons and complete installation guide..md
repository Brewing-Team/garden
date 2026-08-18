---
title: "Debian 12 KDE Plasma: The right GNU/Linux distribution for professional digital painting in 2024. Reasons and complete installation guide."
source: "https://www.davidrevoy.com/article1030/debian-12-kde-plasma-2024-install-guide"
author:
  - "[[David REVOY]]"
published: 2024-05-30
created: 2025-09-27
description:
tags:
  - "clippings"
---
#### Table of Contents

  
  

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_01_thumbnail.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_01_thumbnail.jpg)  
*Fig0. Photo of my workplace, my cat Noutti (my main inspiration for Carrot) says hello!*

## 1\. Introduction

Hey, here is my GNU/Linux Distribution Guide of the Year!  
You can reproduce my professional workstation identically and for free with this guide.  
This is a tradition on my blog, and something I've been publishing .

### A. Motivations:

I wrote this post-installation guide because nowadays I just need this kind of guide in my bookmarks ready to share. I'm crawling under emails, PMs, social media quotes from new GNU/Linux users lost in trying lots of things that don't work. And with Microsoft accelerating the enshitification of its platform with AI, everything is accelerating at the moment. Many users are trying to find a new home.

### B. Target audience:

I'm writing this guide for a specific audience, those who aspire to be or are already **professional** at creating computer graphics. I'm talking about digital painters, CG artists, graphic artists, game developers, illustrators, comic artists, and designers. It's an audience often equipped with powerful PC workstations, sometimes multiple monitors, a graphics tablet (sometimes with a built-in monitor), and a colorimeter. They need a color-managed workflow, a graphical interface to set up their graphic tablet, and their installation needs to be robust in production. They also often have cameras and microphones. They record their process, do live streaming, and edit video.

## 2\. The challenges and the issues

In all these years, I have never seen the GNU/Linux distribution landscape regress so far away from our needs. It is **almost impossible** to find a distribution where you can professionally run and set up **our most basic tools**: Creative software, graphic pen tablet, color calibration. And I tested a wide range of GNU/Linux distributions to make this guide! The choice we have in 2024 is **super limited**.

I can no longer even recommend the distro I used on [my previous guide](https://www.davidrevoy.com/article913/fedora-36-kde-spin-for-a-digital-painting-workstation-reasons-and-post-install-guide), "Fedora KDE spin", because of too many regressions. I tried to [discuss it](https://discuss.kde.org/t/fedora-kde-40-plans-to-completely-drop-x11/5047) way ahead, but very few happened. I even felt kicked out of the Fedora ecosystem...

### A. Three major problems:

#### 1\. Wayland

Wayland is a replacement for the X11 windowing system protocol that is now the default on most distributions. It brings many superior features for solving screen tearing, improves security, and is easier to develop, extend, and maintain than X11. Unfortunately, this switch led to a major rewrite from scratch of the setup of graphics tablets and color management, and this is now completely delegated to the desktop environment. The universal command line interface xsetwacom, which is desktop environment agnostic, has been deprecated. Now the only way to setup many professional aspects of Graphics Tablets (and setup many non-Wacom tablets) is only through the GUI of the Desktop Environment. It's now up to each desktop environment project (e.g. GNOME or KDE Plasma) to develop their own full featured GUI for tablet configuration. The same goes for applying color management to displays. There is no longer a command-line alternative with all options available if the interface doesn't provide the options.

Update 2024-06-08: After reading this article, Peter Hutterer contacted me for questions. Our discussion inspired him [gsetwacom](https://who-t.blogspot.com/2024/06/goodbye-xsetwacom-hello-gsetwacom.html), a Wayland successor to xsetwacom. It's a good news, but this CLI tool will be available for GNOME only, because under Wayland each Desktop Environment will need to code their own.

Update 2024-06-13: The KDE developer Redstrate [annunced](https://framapiaf.org/@redstrate@mastodon.art/112611029799222717) the project [ktabletconfig](https://invent.kde.org/redstrate/ktabletconfig), a CLI utility to change tablet configuration on the KDE Plasma Desktop, inspired by the recent [gsetwacom](https://who-t.blogspot.com/2024/06/goodbye-xsetwacom-hello-gsetwacom.html).

#### 2\. KDE Plasma 6

KDE Plasma 6, this sixth generation was built for Wayland. The previously full featured Graphics Tablets configuration plugin of KDE Plasma 5 was completely deprecated and it was decided to rewrite it from scratch. Unfortunately, only 25% of the features were ported before the first release of Plasma 6. Now KDE Plasma 6 has less features than GNOME based ones, and not enough features for me to even configure any of my tablets for digital painting.

Update 2024-06-08: An addition that needs to be made here, thanks to [this comment](https://floss.social/@carlschwan/112530860048685522) from KDE developer Carl Schwan. I was wrong in the previous paragraph. Plasma 6 can also run on X11, and more surprisingly, KDE Plasma 5's previously full-featured graphics tablet configuration plugin has been adapted for Plasma 6 and can run on it. But it is only for Plasma 6 running under X11 session, the plugin will not work under Wayland session.

#### 3\. Krita

Krita, my main tool for digital art, became too difficult to compile with all its dependencies for packagers, with all the patches and correct dependency versions. Community packages like Snaps, Flatpak or the one proposed by your GNU/Linux distributions can be unstable and introduce bugs (if not sometimes remove features altogether). The Krita developers recommend their Appimage package, distributed on their website: it packs all the fine tuning of dependencies patched to get the best performance, stability out of Krita. Unfortunately, for many new users, the appimage is hard to integrate into the desktop environment: you get a startup icon in your main menu, and the file associations are missing in the file explorer. And it's hard to know that you need the appimage if you don't have the information. New users often just open the Software Center application of their new GNU/Linux distribution, search for Krita, and try that solution first. Something low quality and not representative of what Krita can do. The cherry on top; Krita wasn't written for Wayland. While Krita will run as an Xwayland application under a Wayland session, Wayland will do nothing but introduce performance issues, color management problems, and more bugs. In order to run natively on Wayland, the Krita team would have to go through a refactor, but there are ongoing color management conflicts with the Wayland team, and everything is paralyzed right now, as far as I know. So Krita is still an X11 application.

For more details, MR, and links to specific issues, you'll find [a page that tracks them here](https://community.kde.org/Plasma/Wayland_Known_Significant_Issues), (see the "Color Management" and "Graphics Tablet Support" chapters).

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_02_Tablet-Wayland-versus-X11.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_02_Tablet-Wayland-versus-X11.jpg)  
*fig1. Graphics Tablet interface comparison: Wayland Plasma 6 vs X11 Plasma 5*

### B. Couldn't you prevent this situation?

A small group I was a part of saw this coming for years and we were vocal about it. All of these issues were discussed to avoid the situation I am describing today. But it wasn't enough. We were told that our use was niche, our needs were diminished. Only a small percentage of what was deemed "good enough" has been done and released as is. Presumably, the decision was made to get the advanced functionality down the road, incrementally.

But these three problems are not just little problems: and as I see it, and as I estimate the working force present, I can feel that they are here to stay. Maybe for the next few years.

The risk: This ecosystem might repel professional CG artists who are just trying to install their first Linux distribution alone. After testing what is currently installed by default, they will see the GNU/Linux alternative as a joke.

It hurts, it's a bad result regarding everything I've advocated on this blog for over a decade. This situation is draining my energy...

### C. To the commenters

I have no doubt that I will collect comments along the lines of:

- "But it works for me! I'm on Wayland and I can draw with Krita \[...\]".
- "You should try xxxxx, I heard it works."
- "What about xxxxx?"

To be clear, with simple enough hardware, if you don't bother with color management, if you don't own a colorimeter, and with limited use of CG software, you will probably like what is available on modern mainstream GNU/Linux distributions, and may even find it good enough. There is also a [survivorship bias](https://en.wikipedia.org/wiki/Survivorship_bias), especially if you are among the small percentage of lucky owners of graphic tablets that work out of the box.

### D. To the haters

I'm not against Wayland. I want to adopt Wayland, I want it to succeed. I also want a good, easy and premium experience for Plasma 6 for color management and graphic tablet, and I want the Snap, Flatpak or any distro package to compile Krita correctly.

That's why I spend so much of my personal time on feedback (forums/bug reports) and I will continue to do so. If you are a developer working on it: I strongly encourage your work and I'm open to new ideas. I'm also willing to do beta testing. You know that.

## 3\. Why Debian 12 "Bookworm" with KDE Plasma?

You may want to know my reasons behind this choice, and to sum up, I had to find a distro with:

1. **X11 session**, required to run Krita.
2. **KDE Plasma 5.27.x**, with the Plasma 5 package `kcm_wacomtablet` (the full featured graphical tablet interface).
3. **LTS**, meaning long-term support, because as I said, solving the three problems and challenges could take a long time and years Debian 12 has an end of life estimated at June 2028 according to [this table on wikipedia](https://en.wikipedia.org/wiki/Debian_version_history#Release_table).

I'm also happy to see my research synchronized with the result published by Raghavendra Kamath ["Setting up Debian Linux with Btrfs, KDE Plasma for a creative workstation"](https://raghukamath.com/setting-up-debian-linux-with-btrfs-kde-plasma-for-a-creative-workstation/) in late 2023.

Update 2024-06-09: If you need "up-to-date" development libraries or fresher packages in general for your development work and Debian Stable feels too old, you can use Debian Testing: someone pointed out in the comments that Debian Testing has very similar package versions to Fedora. [A table on Distrowatch](https://distrowatch.com/dwres.php?firstlist=debian&secondlist=fedora&firstversions=1&secondversions=1&resource=compare-packages&view=major&refresh=Refresh) put that in evidence if you want to check.

Update 2024-06-09: If you need a newer kernel on Debian for the latest support for newer hardware, you can install [the Liquorix kernel](https://liquorix.net/).

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_03_why-bookworm.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_03_why-bookworm.jpg)  
*fig2. An illustration I made and published when Bookworm was released.*

About other possibilities, on all my researches I found only [Kubuntu 24.04LTS](https://kubuntu.org/news/kubuntu-24-04-lts-noble-numbat-released/) also compatible with my requirements. But I personally don't like the way Cannonical pushed Snapcraft to the user (a package format). Mainly because of the closed source nature of the snap store, security issues, low quality of their packages. I left Kubuntu Linux 20.04 for Fedora KDE 36 for this very reason after being a Kubuntu user for years.

Update 2024-05-31: As a consequence of the edit in "2.A.2, Problems with Plasma 6" (the fact that Plasma 6 can run on X11, and that the tablet plugin from Plasma 5 has been adapted) opens the door to more possibilities for GNU/Linux distributions. For example, it has been reported in the comments that you can do this combination of components on [Arch](https://archlinux.org/) and Arch-based distributions like [Manjaro](https://manjaro.org/). An Ubuntu-based KDE distribution like [Tuxedo OS](https://www.tuxedocomputers.com/en/TUXEDO-OS_1.tuxedo) sounds like a good choice here, and enthusiasts of [OpenSuse](https://www.opensuse.org/) Leap or Tumbleweed wrote me a word that it was possible.

## 4\. Installation:

### A. Not an installation guide

My page is not an installation guide, but a post-installation guide. You'll find many resources online: [official manual](https://wiki.debian.org/DebianInstall), [articles for Windows users](https://linuxsimply.com/linux-basics/os-installation/single-os/debian/), videos if you search for them on Youtube).

In short, you'll download an ISO file, and you'll need a USB pen drive to write that ISO to. Then you'll plug it into your computer and boot the machine into the system on the USB pen drive. Before you do anything, I recommend that you make a solid backup of all your data.

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_04-install.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_04-install.jpg)  
*fig3. The first screen after booting the ISO.*

### B. About my setup and strategies for installing

If you are curious about my installation, I ran into [a problem with my display](https://unix.stackexchange.com/questions/469753/display-related-problems-during-debian-installation) in the menu of the ISO, and [this answer](https://unix.stackexchange.com/a/699917) solved it for me. It wasn't a sweet welcome in Debian world for me to meet such a major bug right from my first click with it, but everything went ok after that. You might experience similar moments, on different aspect.

**Be persistent, it is worth it.**

It's a good strategy to be equipped with a cell phone, tablet or spare laptop in parallel to your installation. You can search online, read a user guide, browse the official manual, etc.

You will also learn a lot of information about your hardware: the UEFI/BIOS key to set it up, your partitions, etc. This knowledge can quickly fade away because we don't reinstall our systems every month. So I recommend that you log your steps in a text editor or on a piece of paper. This kind of self-documentation will be super valuable for your future, and will give you confidence that you can do it all again if something goes wrong.

For my partitions and filesystem, I did something pretty classic. I chose the 'manual' partitioner, and created

- an Ext4 root "/" for the operating system, 120GB, bootable.
- a swap of 32GB (= the size of my RAM)
- The rest for an Ext4 "/home" for my data.

About my hardware ([more info here](https://www.davidrevoy.com/article806/review-my-digital-painting-workstation-pc-on-gnu-linux)):

- **CPU:** AMD Ryzen 7 3700X
- **Motherboard:** Asrock B450M-Pro4
- **Ram: 4x8GB** G.Skill DDR4 @ 3200Mhz
- **GPU:** Sapphire Radeon RX 5500 XT 8GB
- **Monitors:** 2x Philips 245E QuadHD 24 inch 2560x1440, Color space ability: almost full sRGB.
- **Graphic Tablet:** XPPen Artist Pro 16 (Gen 2), [my review is here](https://www.davidrevoy.com/article1004/xppen-artist-pro-16-gen-2-review-on-gnulinux).
- **Colorimeter:** Xrite Colormunki Smile.
- **Webcam:** Logitech HD 1080p.
- **Camera:** Sony Alpha 6400, connected with an Elgato CamLink.
- **Microphone:** Samson USB Meteor condenser.

### C. No root password, but a user with sudo privileges

Just one important point in the installation process. The installer will ask you at one point to define a root password. It also mentions that you can leave this field blank, and then the admin privileges will go to the user (you). This is probably what you'll want if you want to use sudo from your username in future installs without having to configure it manually.

That's not a behavior I met on Fedora, Kubuntu or Linux Mint KDE: their installer give automatically sudo privilege to the first user. So, if you want the same type of familiar config, leave this one blank (it feels a bit weird).

### D. Install the KDE desktop.

The Debian 12 installer has a single interface for installing many desktop environments. At one point in the process, you'll only need to uncheck the default GNOME and check the Plasma KDE desktop.

### E. Switch to X11 at login screen

Once the installation process is complete, you'll reboot. Before you get to your new desktop, you'll see a login screen. Check a button in the lower left corner of the screen and change from Wayland (default) to X11. You'll only need to do this once. Then log in.

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_04_login-into_X11.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_04_login-into_X11.jpg)  
*fig4. A photo of the X11 option, hidden in a corner of the login screen.*

## 5\. KDE Plasma Desktop Environment Setup

There are many Plasma KDE defaults I don't like, or I couldn't adapt to right out of the box. For me, it's one of the big weaknesses of this desktop environment. Well, I should say "about this version of the desktop environment" because many of these issues have been properly addressed in Plasma 6, and that's promising. But in the meantime, we are on Plasma 5. But its system settings are a gold mine where you can turn almost any problem you encounter into the behavior you're looking for. Do not hesitate to look for a solution to any of your ideas or frustrations: it's likely that KDE Plasma has an option for it.

### A. Graphics Tablet setup

The full featured module for the configuration of Graphic tablet isn't preinstalled by default. but you can quickly install it with:

```
sudo apt install kde-config-tablet
```

Once done, you'll find the options in your Settings, under Device. With this interface, you can create profile, switch between profile with your keyboard, assign complex shortcuts to your stylus buttons, or buttons of the tablet and map the tablet on the display of your choice and in the geometry of your choice. You can even change the pressure curve and calibrate your stylus.

If your tablet is not supported, you can remove this module. I list on this blog many article on how to install [various tablet I own](https://www.davidrevoy.com/index.php?tag/hardware).

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_A.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_A.jpg)  
*fig5a. Graphic tablet panel: General and profile*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_B.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_B.jpg)  
*fig5b. Graphic tablet panel: Stylus options*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_C.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_C.jpg)  
*fig5c. Graphic tablet panel: Buttons*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_D.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_graphics-tablet_D.jpg)  
*fig5d. Graphic tablet panel: Mapping and calibration*

### B. Color Management

The Color Management module is not installed by default, it can apply ICC to your monitors, but cannot profile. My suggestion is to install the excellent DispCalGUI to create ICC profiles and calibrate your monitors with a calibrator.

```
sudo apt install dispcalgui colord-kde argyll
```

You can also calibrate/profile your monitor and apply the ICC using the command line on X11. I describe this in [my previous installation guide](https://www.davidrevoy.com/article913/fedora-36-kde-spin-for-a-digital-painting-workstation-reasons-and-post-install-guide).

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_color-kde.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_color-kde.jpg)  
*fig6a. The Color Management panel*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_displaycal.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_displaycal.jpg)  
*fig6b. Color profiling with my colorimeter and DispcalGUI*

### C. Theme

Breeze, the default theme has a bluish gray tint to it, and that can confuse your sense of color balance a bit. It's minor: the most important thing is still the theme of your creative application. But it's a nice touch to be able to make the entire O.S. 'neutral', especially if you profile/calibrate your monitors with a colorimeter and like to check your image thumbnails in the file explorer, Dolphin.

Here is my setup, you can reproduce it with the button "Get New \[...\]" on the settings

- Appearance > Plasma Style: **Unity-Plasma**.
- Appearance > Colors: **Breeze Dark Neutral**.
- Appearance > Colors: You can set a customized color accent to match your mood or wallpaper.
- Appearance > Cursor: **Adwaita**.
- Appearance > Windows Decoration: Breeze (click small edit icons on thumbnail). **Button size > small**.
- Appearance > Windows Decoration: on the top, tab named "Titlebar Buttons", remove the icon on the left.

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_Breeze-dark-neutral.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_Breeze-dark-neutral.jpg)  
*fig7. Theming options*

### D. Plasma setup

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_KDE-Plasma-appaerence.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_KDE-Plasma-appaerence.jpg)  
*fig8. A screenshot of two of my display (click to enlarge)*

#### 1\. Wallpaper and desktop

Right-click on the background image and you'll find a menu to configure your wallpaper. By default it has a folder view on your /home/username folder. A strange choice, so I remove that to a layout: Desktop, and a wallpaper of my choice (you can add your own images). If you want the same I have in my screenshot here, [this wallpaper is here](https://wall.alphacoders.com/big.php?i=263775).

#### 2\. Panels

For my panel, I right click on an empty part of it and select "Enter Edit Mode". It has an option to move it to the top of my screen, I also reduce its height to 30px.

You can press the "+Add widget" button to add new options to your panel. I like the Color Picker widget here, and I prefer the "Task Manager" to manage my windows (showing the name as a label) over the icon-only task list. I later set the Task Manager (in edit mode, an option when you hover over it) not to group similar windows and to show only the windows of the current screen. I do this because I have two monitors and each of them has its own panel and a task manager that shows only the windows open on the current monitor.

Another button I like on my panel is the Overview button, it shows an overview of all open windows. However, it is not installed by default. You'll have to find it and install it using the "Get New Widget" button in the widget menu.

For my main menu icon, I just use a homemade [thickened Debian logo PNG](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/debian-logo-thick.png). Thickened, because it looks better once reduced as an icon.

#### 3\. Virtual Desktops

I also have a pager with four virtual desktops "prod", "dev", "writing" and "tmp". It's useful when I'm producing an artwork (virtual desktop "prod"), but I have an idea for a new scenario. I can quickly switch to the "writing" virtual desktop with my text editor already open, all my characters, locations, timeline document, my online dictionary tab open, etc. The 'dev' is the one that always has everything to render the Pepper&Carrot translation, manage the websites, and change my setup. The 'tmp' is an empty one, useful when I need to record a video segment with a clean looking interface.

#### 4\. Don't drag/move windows from empty part

By default, Plasma allows you to drag windows by clicking on an empty part of their UI. Unfortunately, this behavior is dangerous when drawing with a tablet: a long line on Krita going out of the UI can drag the whole Krita interface almost out of your screen.

To fix this, go to Appearance > Application Style, and look for a little 'edit pencil' in the corner of the Breeze thumbnail. The option is called Windows drag mode: from title bar only.

#### 5\. Disable the Hot Corner/Screen Edge.

By default, you can 'hit' the top left corner of the screen with your mouse or touchpad (something you can't do with a graphic tablet) and Plasma will go into overview mode. I never like this behavior: I accidentally trigger it.

Go to Workspace Behavior > Screen Edges and set the little white square to "no action".

In many situations, Plasma will darken the entire interface (grayscale, turns it black and white) when a modal dialog pops up. It can be a file manager to open or save a file, or any dialog that needs your attention. While I understand the concept, it's often counterproductive: because many of these dialogs can still be related to the information you need to access and read in windows that are 'shaded in the background'. So it is better to remove this effect.

Workspace Behavior > Desktop Effect > Remove "Dialog Parent" in Focus.

### E. Dolphin, the file explorer

A lot of thumbnail previews are enabled by default and this is good (in Configure, General -> Preview). You'll have Krita files, Tiff, PDF, JPG, PNG, etc... and with a possibility to see them large. A very useful tool if you work with images all day.

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_dolphin-thumbnails.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_dolphin-thumbnails.jpg)  
*fig9a. Dolphin: many thumbnail image format support.*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_dolphin-thumbnails-series.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_05_dolphin-thumbnails-series.jpg)  
*fig9b. Dolphin: large thumbnails, ideal to do triage visually.*

#### 1\. Double click to open directories and files

I prefer to open files by double-clicking on them, and this is not the default behavior of Plasma 5. To set this, go to System Preferences > "Workspace Behavior" -> "General Behavior", Clicking files or folders: check "Select" instead of "Open".

#### 2\. Directory thumbnails

I dislike the four small thumbnails at the top of my folder icons: they are supposed to show four images in their content, but I find it visually unappealing and it rarely gives me a faster navigation reflexe. To disable them, go to Dolphin, Configure, General -> Preview and uncheck "Folders".

#### 3\. Display the full Path

I also like to see the full path in the location bar of my current directory view. To restore this, go to Dolphin Preferences, Startup > (check) Show full path within location bar.

#### 4\. Git Previews

If you work with Git repositories on your project, you might be interested in getting little icons in Dolphin to indicate that your files have been changed, committed, updated, etc. To install this,

```
sudo apt install dolphin-plugins
```

Then go to Configure > Context Menu > and check the "Git" checkbox. Then close all Dolphin instances and restart them.

## 6\. The Software

The GNU/Linux ecosystem has thousands of pieces of software available for installation. Here is a list of what I use, if you need inspiration or are new to this.

**Beginner's tip:** To copy a command line here, `<ctrl>+C`, but to paste it into the console it's a bit more complex: `<ctrl><shift>+V`.

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_krita.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_krita.jpg)  
*fig10a. Screenshot while running Krita.*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_inkscape.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_inkscape.jpg)  
*fig10b. Screenshot while running Inkscape.*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_kdenlive-obs.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_kdenlive-obs.jpg)  
*fig10c. Screenshot while running Kdenlive and OBS studio.*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_fontforge_audacity.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_fontforge_audacity.jpg)  
*fig10d. Screenshot while running Fontforge and Audacity.*

[![](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_scribus.jpg)](https://www.davidrevoy.com/data/images/blog/2024/debian-kde/2024-05-30_06_scribus.jpg)  
*fig10e. Screenshot while running Scribus and Neofetch.*

### A. To keep

Software that is already installed by Debian KDE 12 and that I like to use.

- [okular](https://okular.kde.org/) A solid PDF reader.
- [kontrast](https://apps.kde.org/kontrast/) A small application to check the contrast between colors, useful to check the contrast of a text on any colored background.
- [libreoffice](https://www.libreoffice.org/) The full suite with calc, writer, draw, etc.. Useful for many tasks.
- [ark](https://apps.kde.org/ark/) A tool to manage all compressed archives, zip, tar.gz, bzip2, rar, etc...
- [kwrite](https://en.wikipedia.org/wiki/KWrite) A lightweight text editor. I usually don't use it and open everything in kate, but it doesn't hurt to have it.
- [kate](https://apps.kde.org/kate/) Writing, coding, I use kate for everything and have developed a deep love for this software. I especially like the customization of the color syntax and the theming possibilities.
- [gimp](https://www.gimp.org/) I rarely use it these days, but I keep it as a Swiss Army Knife tool in case I run into a weird case of image encoding.

### B. To install using apt (Debian packages)

Here is a list of what I install directly from the \*.deb packages of the Debian stable repositories using \`apt' this way:

```
sudo apt install mc micro zim qimgv audacity audacious clementine vlc treesheets gnome-disk-utility meld fontforge peek filezilla konversation inkscape scribus krename xournal
```
- [mc](https://en.wikipedia.org/wiki/Midnight_Commander): Midnight Commander, a CLI file explorer, because I like to manage files with it sometimes, especially when moving large chunks from drive to drive.
- [micro](https://micro-editor.github.io/): a CLI text editor, "sudo micro" is my go-to when I need to edit config files. It has Ctrl+C, Ctrl+V, Ctrl+Q and Ctrl+S kind of reasonable shortcuts.
- [zim](https://zim-wiki.org/): my local wiki, where I write a lot of personal manuals. They often get turned into tutorials on my blog later.
- [qimgv](https://github.com/easymodo/qimgv): my favorite image viewer, it doesn't have many fancy options, but it's lightning fast.
- [audacity](https://www.audacityteam.org/): Swiss Knife advanced audio editor, I use it to edit voice over recordings for my tutorials, or when I need to change sound fx for my videos.
- [audacious](https://audacious-media-player.org/): An audio player, I use it to quickly listen to wav and mp3 on the fly while recording. I also like its support with plugins ( audacious-plugins ) for old console sound emulation.
- [clementine](https://www.clementine-player.org/): Everyone has their favourite audio player, here I still love Clementine: it has a precise visualization of the song timeline, I can navigate long songs with comfort.
- [vlc](https://www.videolan.org/vlc/): VLC Media Player, the famous video player. It's probably the only software I know that accompanied my computer system before 2000. An old friend.
- [treesheets](https://strlen.com/treesheets/): a free form data organizer, I use it for brainstorming and mind mapping when I do scenarios.
- [gnome-disk-utility](https://apps.gnome.org/DiskUtility/): a tool to manage hard disk, SSD, pen drive, burn ISO, etc. I really like the features and clarity of this application.
- [meld](https://meldmerge.org/): A tool to compare two or three plain text files. I use it to compare scenarios, but also code, svgs, etc.
- [fontforge](https://fontforge.org/en-US/): A tool for editing or creating fonts.
- [peek](https://github.com/phw/peek) A small application that can take a short screenshot of a region of the screen as a gif. Great for tutorials or bug reports.
- [filezilla](https://filezilla-project.org/): A tool I have been using for probably 20 years. Publishers, studios, clients, delivering files via sFTP is still a professional standard.
- [konversation](https://konversation.kde.org/): A full-featured IRC client for Plasma.
- [inkscape](https://inkscape.org/): The vector drawing tool of choice, a big part of my comics (for speech bubbles and text).
- [scribus](http://www.scribus.us/): A desktop publishing tool I use for the printed books of Pepper&Carrot.
- [krename](https://apps.kde.org/krename/): Sometimes you need to prefix or suffix a lot of files, or delete the same pattern between them. krename does all this very well.
- [xournal](https://xournalpp.github.io/): I use it to edit PDFs, more specifically to draw on them. Useful for signing paper, filling out forms without having to print them, filling them out and scanning them.
- [neofetch](https://github.com/dylanaraps/neofetch): If you type 'neofetch' in the console after installing this package, you'll get information about your system.

### C. To install as Flatpak:

Flatpaks are packages that can install the latest version regardless of your operating system. That's what makes this Debian KDE a good choice.

Once installed, you'll have access to the whole catalog of applications from [Flathub](https://flathub.org/). But you'll also find them in Discover, the built-in application center.

#### 1\. Installation of the Flatpak system

```
sudo apt install flatpak plasma-discover-backend-flatpak kde-config-flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

Then reboot the system.

#### 2\. Flatpaks I install

To install applications, I just search for their names in Discover and manually install them one by one.

Be careful: a software might have multiple sources in Discover (e.g. a Debian package and a Flatpak). A "Source" button will appear in the upper right corner of the software's page in Discover.

Click on it and select "Flathub" instead of "Debian deb". This is important because the Debian package will be an older version and will be frozen at that version. With the Flatpak, on the other hand, you'll have access to the latest release.

- [BeeRef](https://flathub.org/apps/org.beeref.BeeRef): a tool for managing image references.
- [Nomacs](https://flathub.org/apps/org.nomacs.ImageLounge): an image viewer, I use it as a secondary one for certain options (like the ability to keep the zoom while browsing a series with the same resolution).
- [Kdenlive](https://flathub.org/apps/org.kde.kdenlive): My favorite video editor, for all the videos I make for my Youtube and Peertube channel.
- [OBS Studio](https://flathub.org/apps/com.obsproject.Studio): Screen capture and audio capture, it also handles livestreaming.
- [Blender](https://www.blender.org/): THE 3D software, I use it mainly to do mockup of my landscape, interiors, as a helper to draw or paint over my rendering later.
- [Video Trimmer](https://apps.gnome.org/VideoTrimmer/): A small application to quickly cut the beginning and end of a video without re-encoding.
- [Identity](https://apps.gnome.org/en/Identity/): A small application able to compare images and videos. Useful for analyzing compression.
- [Detwinner](https://neatdecisions.com/products/detwinner-linux/): Find and manage duplicate files. A cleaning tool, useful when merging a lot of data.
- [Signal](https://www.signal.org/): A messaging client, some groups I follow are exclusively on it.
- [Nextcloud](https://nextcloud.com/): I have a small (also Debian Bookworm) server at home, Nextcloud is on it; with this desktop application I can synchronize the directory on my machine with the server.

#### 3\. Configuring Flatpaks permissions

Thanks to the `kde-config-flatpak` package, you'll have an interface in System Preferences > Applications > Flatpak permissions settings that allows you to manage the permissions for all your installed flatpaks: how they can access your disk, devices, etc.

#### 4\. How to survive a broken Flatpak update?

If a newer update of a Flatpak is problematic or broken (it happens), the Flatpak provides you with command-line options to "roll back" the package to an earlier version. Here is how to do:

First, we need to find the application name ID, because Flatpak names are complex (eg. org.kde.kdenlive for kdenlive):

```
flatpak list
```

Then list the available versions you can roll back to (commit). Eg. here for Kdenlive:

```
flatpak remote-info --log flathub org.kde.kdenlive
```

Copy the interesting commit number and set it this way:

```
flatpak update --commit=ec07ad6c54e803d1428e5580426a41315e50a14376af033458e7a65bfb2b64f0 org.kde.kdenlive
```

Done, you can test your Flatpak at your favorite version. But a problem: your update manager (built in Discover) will inform you an update is available for Kdenlive now: you are using an old version! To prevent the package to update to the broken new version, you have to mask it:

```
flatpak mask org.kde.kdenlive
```

Now inform the developper of the problem ([here is how I do it](https://github.com/flathub/org.beeref.BeeRef/issues/62)) because if no one report the issue, it will likely persists forever. Once the problem is fixed, you can test and remove the mask:

```
flatpak mask --remove org.kde.kdenlive
```

### D. Krita as appimage

As I wrote in the introduction, if you install Krita from the app store (Discover) via apt or flatpak, you might not get an optimal version. The Krita team packages a version itself and tests it under the appimage format. So if you want the best quality and fewer bugs, you'll need to [download the latest appimage from krita.org](https://krita.org/en/download/).

Unfortunately, appimage packages don't have the best and easiest system integration. To run an appimage, you just have to right click on it, Properties, Permission (tab), and check "is executable". After that, press OK, and double click the appimage to run it. Easy.

A right click on the main menu of Plasma (your application launcher) will allow you to "Edit application", and here you can create a launcher for your appimage, for convenience.

You will also have to manually manage the file association. Find a Krita kra file, right click on it, go to `Properties` and in the tab `General` locate the button `Change`. In this dialog you can `+ Add` applications to the list, and decide their order. That's how you have your Krita file associated for Krita appimage in Dolphin. I often do this for all my images format, tiff, png, jpg, etc... (they open directly with my viewer; qimgv, and the second choice is Krita to edit them).

### E. Default applications I remove:

Once I have all my usual software, I no longer need some of the pre-installed defaults. So I uninstall them.

```
sudo apt remove gwenview juk dragonplayer kmail pim-sieve-editor
```
- [gwenview](https://en.wikipedia.org/wiki/Gwenview): The standard image viewer. Thick interface, weird icon, difficult to navigate with the middle mouse button (panning with it pressed, zooming with scrolling). I prefer qimgv.
- [juk](https://juk.kde.org/): The default music player, it is crude in features compared to Clementine.
- [dragonplayer](https://apps.kde.org/dragonplayer/): The default video player, crude in features and a bit too big an interface around the media; it feels a bit like an old-school Windows Media Player. Too bad, I like the name of it.
- [kmail](https://apps.kde.org/kmail2/): The default email client, probably good, but I use ProtonMail webmail, so not necessary for me. (also to remove: pim-sieve-editor)

While installing my system, I had to do a few things that were specific to my needs or my hardware. **These are not things you'll do during your installation**, but I prefer to write them here so I can remember what I did, and believe it or not, they are sometimes useful for others as well. At least, it was when search engines referenced my tips.

### 1\. Updating the kernel

If your machine is more modern than the kernel included in Debian 12 (6.1), know that you won't be blocked. You have the option to upgrade your kernel (at your own risk). The [backport repository](https://backports.debian.org/) is secure by reputation and contains many kernels. Also, projects like [Liquorix](https://liquorix.net/) can give you the latest.

Eg. for applying very specific [udev-hid-bpf](https://gitlab.freedesktop.org/libevdev/udev-hid-bpf) workaround for my beloved [XpPen Artist 16 Pro Gen 2](https://www.davidrevoy.com/article1004/xppen-artist-pro-16-gen-2-review-on-gnulinux), I had to adopt the [Liquorix](https://liquorix.net/) kernel (6.8.10-2-liquorix-amd64).

### 2\. Fix wrong directory colors in Dolphin (not following accent color).

This can happen if you were on another KDE Plasma desktop before, or if you tweaked your previous desktop too much. For some reason, I had many folders colored, but as "hardcoded color" with the folder gray icon as default. This was problematic because these folders couldn't follow the accent color option in Appearance > Color.

First, I did a reset of my.directory files on my entire hard drive, these hidden files created by Dolphin store many folder customizations. Be careful with this command, they will all be deleted recursively:

```
find . ( -name ".directory" ) -delete
```

Then I went to Settings > Application > File Association, and in inode (directory) I find the icon "folder" for them.

### 3\. Python3 → Python

The Python executable is named `/user/bin/python3` on Debian, so any scripts that try to find a `python` executable will fail with `/usr/bin/env: ‘python’: Permission denied`.

Since I was coming from an operating system that 'evolved' and only called python3 'python', I decided to restore a path to it using a symbolic link:

```
sudo ln -s /usr/bin/python3 /usr/bin/python
```

(update thanks to the comments: an apt package actually exist for that: `python-is-python3` )

### 4\. Git config

Debian will create a username, a mail address for you to interact with Git, it will also ask for your password everytime. To re-setup that manually:

```
git config --global user.name "FirstNameHere LastNameHere"
git config --global user.email Your@public-email.com
git config --global credential.helper store
```

## 8\. Conclusion

I've only been using this operating system for two weeks. So, a word of caution: I can't publish a tutorial with a full year of testing. But these last two weeks have been intense, and I had to test almost all parts of my installation (except starting a real livestream, but everything looks ready on OBS studio). I have already been productive with it and from my experience this is a really polished system. Bravo to all the decisions behind this Debian Bookworm 12.

I hope you enjoyed these instructions!