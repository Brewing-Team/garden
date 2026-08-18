---
title: "You're streaming your games wrong, let me show you the optimal way (MoonDeck)"
source: "https://www.reddit.com/r/SteamDeck/comments/19ahzxq/youre_streaming_your_games_wrong_let_me_show_you/"
author:
  - "[[Tpdanny]]"
published: 2024-01-19
created: 2025-06-16
description:
tags:
  - "clippings"
---
**TL:DR / why should I care? Here is a video of me demonstrating the setup:** [**https://youtu.be/MDy1EPJhnKY**](https://youtu.be/MDy1EPJhnKY)

Many of us who own Steam Decks also own powerful PCs, but perhaps prefer the handheld form factor for gaming for any number of reasons (convenience, kids, etc). As a result our PCs gather dust, and we use the Deck.

However, the Deck cannot play games to any way near the same graphical quality as the PCs we used to mainly use as it lacks the horsepower. To this, Valve provides a solution - Steam Link. Steam Link allows you to conveniently select your main PC as the host for a video stream to your Deck as the client, over which you stream the game. There are a number of advantages to **Steam Link**:

1. Convenience - you can select it straight from the steam library on your Deck with a built in button.
2. Ease - no, or little, configuration is needed.
3. Graphical power - You use the hardware of your PC to render, so you can have raytracing, ultra settings, etc.
4. Low battery consumption - You're just streaming, therefore you can play high end games for many hours, especially on an OLED deck.

However, there are a number of cons:

1. Latency - Steam Link has a noticable lag
2. Compression - Even if you manually increase the bit rate, the compression used on Steam link is noticable.
3. (Currently fixed in the Preview branch) Image is darker than it should be - A bug on the Stable branch for now.
4. If I need to restart my PC, or shut it down remotely once I'm done, I can't do that.

To the above issues, many would suggest you use **Moonlight** - an alternative streaming option, and they would further suggest you base this on the **Sunshine** hosting tool that you can install on your host PC. Moonlight has a number of advantages over Steam Link:

1. Lower Latency - the latency of a configured Moonlight stream is not noticable over a good home connection.
2. Image quality - There isn't any noticable compression to the image unlike Steam Link if the connection has the bandwidth to support this.
3. Full control of the PC power state - You can turn on, restart, and shut down your PC remotely as needed.

However, again, there are cons:

1. Less convenient - You add Moonlight as an app to your Steam Deck and then boot it up in your library, then connect to your PC via Steam big picture mode, then launch your games. The dedicated 'stream' button is missing.
2. Aspect ratio changes on host PC - In streaming to the Deck, the host PC changes aspect ratio and resolution to 16:10 1280x800, and when the stream ends it doesn't go back to normal without you manually changing it.
3. Controls - Most, if not all the time, the stream expects PC controls you will have to configure, or search for control layouts yourself. The defaults you have come to expect pre-configured on the Steam Deck are not present.

But, what if I told you that **you can have all of the pros of Moonlight, with all of the convenience of Steam Link**, and therefore, none of the downsides. The ultimate streaming solution to play games at maximum settings with ray tracing and no lag or compression artefacts, all launched from a convenient button in your Steam Library on the Deck, and that both devices revert to their normal state when the stream ends. Sounds too good to be true? Well, let me tell you how with this handy guide.

**Step 1 - Standard setup of Sunshine on Host PC**

1. Download Sunshine from here: [https://github.com/LizardByte/Sunshine/releases/tag/v0.21.0](https://github.com/LizardByte/Sunshine/releases/tag/v0.21.0) - pick the file for your system, so if you're using Windows, you want the installer.exe file.
2. Run the .exe, install according to the defaults will be fine.
3. Press the Windows key, type Sunshine and launch - it will now live in your hidden icons on your taskbar. It will ask you to set up a username and password, don't forget these! It will also ask you to name your instance of Sunshine; when doing this, use only numbers, letters, and spaces, *do not use special characters!*
4. Under configuration, enable UPnP, this allows you to stream outside your home, but note this will have more lag and will be dependent on both location's internet speeds.
5. Download Qres from here: [https://www.majorgeeks.com/files/details/qres.html](https://www.majorgeeks.com/files/details/qres.html), extract the file, then copy the .exe and paste it into your Sunshine folder found at C:\\Program Files\\Sunshine
6. On Sunshine, go to Configure, then add a command:
7. Do - paste the following, without quotation marks, changing the square brackets to the value for your Deck: "cmd /C "C:\\Program Files\\Sunshine\\QRes.exe" /x:%SUNSHINE\_CLIENT\_WIDTH% /y:%SUNSHINE\_CLIENT\_HEIGHT% /r:%SUNSHINE\_CLIENT\_FPS%" (thanks [u/snoodelz](https://www.reddit.com/user/snoodelz/))
8. Undo - paste the following, without quotation marks, changing the elements in square brackets to your defaults: "cmd /C "C:\\Program Files\\Sunshine\\QRes.exe" /x:\[your native res\] /y:\[your native res\]/r:\[your native refresh rate"
9. Enable 'Run as admin' by ticking the box.
10. Configure the NVIDIA NVENC Encoder - by default this is P1 and Quarter resolution, you can play with these later depending on your internet speed to get more quality. For now, just know they are here, and increase them later if you have particularly good internet and want to improve the visual quality.
11. Save changes and apply at the bottom of the screen in Sunshine.

**Step 2 - Set up Moonlight on Steam Deck**

1. Switch your Steam Deck to desktop mode by holding the power button and selecting the option in the menu.
2. Opening the default store, type 'Moonlight' - install this application.
3. Launch Moonlight
4. You will see a grey window with a blue header. On that header, click the settings cog.
5. Configure the following:
6. Resolution - Native 1280x800
7. FPS - 60 if using the LCD Deck, 90 if on the OLED
8. Fullscreen
9. Turn off V-sync (I force it on on the host PC and utilise G-sync and a framerate cap, if you're not sure how to optimise for full frames with no stutter or input lag, you could always leave this on).
10. Audio - Stereo
11. Mute host PC - Yes
12. Video decoder - automatic
13. Video codec - automatic
14. Go back to the main screen, connect to your PC, it will ask you for a Pin on the host PC, you click the notification on the host PC and type in the one provided by the Deck. You are now connected, but we can do more...
15. To add moonlight to Steam (this is normally the last step, but we will improve upon this with MoonDeck), open the start menu on the Deck, find Moonlight in the app list, right click it, and add to Steam. Steam will launch and it will now be added.

**Step 3 - Set up DeckyLoader and acquire MoonDeck**

1. To download DeckyLoader and install, you should stay in Desktop mode.
2. Download DeckyLoader by clicking this link: [https://github.com/SteamDeckHomebrew/decky-installer/releases/latest/download/decky\_installer.desktop](https://github.com/SteamDeckHomebrew/decky-installer/releases/latest/download/decky_installer.desktop)
3. In your downloads file, rename the file to "decky\_installer.desktop" without the quotation marks.
4. Drag the file on to your desktop and double click to run it.
5. Either type your admin password or allow Decky to temporarily set your admin password to Decky! (this password will be removed after the installer finishes).
6. Install the latest release.
7. Return to gaming mode by double clicking the icon on your desktop to do so.

**Step 4 - Set up MoonDeck and game**

MoonDeck is an application, provided via the DeckyLoader store (it's all free), which will allow you to bring the convenience and seamless integration of Steam Link to the quality connection of Moonlight.

1. To begin, press the "..." button on the right hand side of your Steam Deck, you will now notice a power plug looking icon on this menu at the bottom, scroll down to select it.
2. On the 'Decky' menu you will see two icons, a store, and a settings cog, click the store cog.
3. Type in 'MoonDeck', install the current version. This can take a while and feel like your deck is hanging, but it's fine, just wait.
4. When you press the "..." button again, you will see MoonDeck as an option, select it, it should say 'HOST IS NOT SELECTED'
5. Click the settings icon, you will now be shown a setup guide, which we will follow:
6. On your host PC, download and install MoonDeck Buddy from here: \[[https://github.com/FrogTheFrog/moondeck-buddy/releases\]](https://github.com/FrogTheFrog/moondeck-buddy/releases])
7. Launch Buddy on the host PC by pressing the Windows key and typing 'MoonDeckBuddy', it will now be added to your hidden icons on your taskbar. Right click it, and select 'Start on system startup'.
8. Back on your Steam Deck, select 'Host selection' on the left hand side of the screen. Scan your local network and pick your instance of Sunshine as Current host.
9. You now need to pair MoonDeckBuddy, select the pair button at the bottom of the screen on your Steam Deck. Go through the pairing process, which will involve getting a pin from one device and entering it on the other.
10. On your PC whilst logged into Sunshine, if MoonDeckBuddy doesn't already show up, add an application by going to 'Applications', click add new. In the name of the application, type "MoonDeckStream" withouth the quotation marks. Nothing in output, global prep commands enabled. Under Command, enter the following without quotation marks, replacing \[user\] with your username: "C:\\Users\\\[user\]\\AppData\\Local\\Programs\\MoonDeckBuddy\\bin\\MoonDeckStream.exe"
11. Under 'Moonlight settings' we will now configure Moonlight, do the following:
	1. Default bitrate - as high as you can get away with, with a maximum of 150,000. For my 1 gigabit connection this is what I use. I would suggest, assuming your PC is wired via ethernet, which I highly suggest you do, whatever your internet speed is as a percentage of 1 gigabit, divide 150,000 by this to find the figure you can safely use.
	2. Default FPS - 60 or 90 dependent on if you have the LCD or the OLED deck.
	3. Pass the resolution to Buddy - toggle on
	4. Pas the resolution, bitrate, etc to Moonlight - toggle on
	5. Use Steam Deck's primary resolution as fallback - toggle on
	6. Selected override - Display resolution
12. Under 'Sunshine Apps' on the left-hand side, select this and then Sync all Sunshine's apps via Buddy.
13. Under 'Game session' on the left-hand side, enable Automatic title switch to AppId and Resume game session after system suspension.

**You are now done!**

When you go to any game page on your Steam Deck, provided the game is installed on your host PC, you will see a moon and stars icon on the right hand side of the header imagery. Click this, your Steam Deck will automatically connect to your PC (if it's on), the PC will change res and aspect ratio, Steam will launch in big picture mode, and the game will start with Steam Input-based controls enabled. When you end your session and quit the game properly, the stream will end and the host PC will return to it's default state as we configured with Qres.

This post was a lot of effort and compiles a lot of info you may want to know - I can try to answer questions if you have them but I'm not the dev of any of these projects, so please be kind. I hope this helps the users willing to put in the half-hour or so of work this takes with powerful PC hardware can now get even more out of their deck than they previously thought possible.

EDIT: To have Steam Big Picture mode close on the host PC when you’re done gaming, go to “Host settings” on MoonDeck, scroll down, and toggle on “Automatically close Steam on host when gaming session ends”. Thanks to those who pointed it out to me, I neglected to mention it as I thought it was a default setting.

---

## Comments

> **Some\_guitarist** • [167 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil1tyh/) • 2024-01-19
> 
> Just to add, if you hate yourself and have a bunch of free time, check out Nonary's github here ([https://github.com/Nonary](https://github.com/Nonary)) for a few solutions to your relatively few Moonlight issues.
> 
> You can set your PC up with a 'fake' monitor using the link in the github, then set the scripts above so that when you use Moonlight to connect from any device (Steam Deck Included!), it'll turn off your desktop monitor, turn on the fake monitor, read the resolution of whatever you're currently using, set the fake monitor to that resolution, and launch the game.
> 
> It'll do the inverse when you exit the game.
> 
> This has a lot of added benefit if you have multiple places you log in from. I have an HDR Ultrawide PC monitor, 4k HDR TV, 1080p laptop, and the HDR OLED Steam Deck. No matter what I'm streaming to, it'll set everything up for me.
> 
> I still have to occasionally go and change the in-game settings to the correct resolution, but the 'Monitor' that it's streaming from will always match!
> 
> EDIT: Also worth mentioning to anyone interested in using Moonlight (it really is seriously better that Steam Link!) you don't need the DeckyLoader and all that! If you just hit 'Restart in Desktop Mode' go to 'Discover' and type in 'Moonlight' it'll be on your desktop. Then just right click on that and hit 'Add to Steam Games'!
> 
> > **icoez** • [11 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kim3w7g/) • 2024-01-19
> > 
> > Do you need a dummy monitor plug to do this?
> > 
> > **carpeggio** • [5 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kiq7v2p/) • 2024-01-20
> > 
> > An alternative to the Nonary's MonitorSwap solution is using DisplayFusion to handle monitor profiles.
> > 
> > Create a Monitor Profile where the virtual IDD monitor is 'Primary' and set to the Res/Hz you want. Name it whatever you want {MOONLIGHT PROFILE NAME}.
> > 
> > Do Command;
> > 
> > > C:\\Program Files (x86)\\DisplayFusion\\DisplayFusionCommand.exe -monitorloadprofile "{MOONLIGHT PROFILE NAME}"
> > 
> > Undo Command;
> > 
> > > C:\\Program Files (x86)\\DisplayFusion\\DisplayFusionCommand.exe -monitorloadprofile "{DEFAULT PROFILE NAME}"
> > 
> > [https://www.displayfusion.com/Discussions/View/displayfusion-command-line-tool-displayfusioncommandexe/?ID=06d90ec9-5e5a-4be2-8540-6b52fbb4536e](https://www.displayfusion.com/Discussions/View/displayfusion-command-line-tool-displayfusioncommandexe/?ID=06d90ec9-5e5a-4be2-8540-6b52fbb4536e)

> **Tpdanny** • [121 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kikwlhu/) • 2024-01-19
> 
> I'll probably make a YouTube tutorial for all of this at some point in the future as most on Youtube for Moonlight are out of date (they use Nvidia game stream), poorly explained, or don't integrate MoonDeck, which is honestly what makes it so much better than default Steam Link. For now, this guide will do.
> 
> If you spot errors, that's because I wrote it largely from memory, but I'll edit it as they're pointed out to me!
> 
> I hope this makes a nice change from the community posts you're used to, I'd love to bring a little more tech discussion back to this subreddit. Please engage with this if you enjoyed it.
> 
> > **Upper-Dark7295** • [8 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kilhqa1/) • 2024-01-19
> > 
> > Doesn't this not work with non-steam games, that's a majority of my PC library. Lots of emulation like PS3.
> > 
> > **waterm3lown** • [4 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kilie8t/) • 2024-01-19
> > 
> > Yesss video tutorial pleeeease!

> **\[deleted\]** • [0 points](https://reddit.com/) • 2024-01-19

> **ScootyPuffJr1999** • [34 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kikyvc2/) • 2024-01-19
> 
> Idk I have never had my pc change aspect ratios after using moonlight normally. I can also turn off my pc just fine through moonlight. Never had to use big picture mode on the host pc either. I stream in 1440p and the deck downscales from a higher resolution so it looks nice.

> **snoodelz** • [14 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kiq5y6c/) • 2024-01-20
> 
> Instead of  
> `cmd /C "C:\Program Files\Sunshine\QRes.exe" /x:1280 /y:800 /r:60`  
> I would recommend  
> `cmd /C "C:\Program Files\Sunshine\QRes.exe" /x:%SUNSHINE_CLIENT_WIDTH% /y:%SUNSHINE_CLIENT_HEIGHT% /r:%SUNSHINE_CLIENT_FPS%`  
> This sets the resolution based on what the moonlight client asks for so it works on multiple resolutions not just the steam deck res i.e. 4k screens, steam deck, laptops.
> 
> It's based on the docs here  
> ([https://docs.lizardbyte.dev/projects/sunshine/en/latest/about/guides/app\_examples.html#windows](https://docs.lizardbyte.dev/projects/sunshine/en/latest/about/guides/app_examples.html#windows))
> 
> > **Tpdanny** • [5 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kq4m29e/) • 2024-02-12
> > 
> > > cmd /C "C:\\Program Files\\Sunshine\\QRes.exe" /x:%SUNSHINE\_CLIENT\_WIDTH% /y:%SUNSHINE\_CLIENT\_HEIGHT% /r:%SUNSHINE\_CLIENT\_FPS%
> > 
> > This is good advice and I'll put it in the post.

> **daggah** • [30 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil28h1/) • 2024-01-19
> 
> > Under configuration, enable UPnP, this allows you to stream outside your home
> 
> From a network security perspective, this is a **very** bad idea. If you want this functionality, UPnP also needs to be enabled on your router, but UPnP is particularly vulnerable and a very juicy target for hackers.
> 
> [What is UPnP? Yes, It's Still Dangerous in 2024 | UpGuard](https://www.upguard.com/blog/what-is-upnp)

> **H3XAntiStyle** • [13 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kikykr4/) • 2024-01-19
> 
> Does it launch specifically the full suite of Steam Deck controls? Trackpads, gyro, and all?

> **SymphonyInPeril** • [11 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil20k5/) • 2024-01-19
> 
> I’m not amazing with stuff like this and I tried to set up MoonLight when I first got my deck and it just didn’t work for me for some reason. I appreciate an in-depth step by step guide like this. I’ll give it a try sometime soon. Thank you for your work!

> **ChillZilla2077** • [7 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil217h/) • 2024-01-19
> 
> I tried moonlight and sunshine but couldn't turn off my monitor without killing the connection, with steam link I can turn off the monitor and still be able to stream just fine

> **hyrumwhite** • [6 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil7eb6/) • 2024-01-19
> 
> Iirc you can setup wake on lan with moonlight right? Lets you turn your pc on with your deck and you can setup auto login too

> **The\_Legend\_of\_Xeno** • [6 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kilrzop/) • 2024-01-19
> 
> We will watch your career with great interest.

> **\[deleted\]** • [6 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kkapzjo/) • 2024-01-30
> 
> Just finished setup and I was thinking, what if I plug my deck into my 4k TV? Will the resolution be streaming at 800p?
> 
> great tutorial btw, thanks.

> **old\_man\_MODOK** • [5 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil9695/) • 2024-01-19
> 
> Shamefully insert my setup from my post a week ago.:
> 
> My SteamDeck use case is the following: for traveling, visiting my girlfriend (LDR) I have some indiegames on my deck installed, thats all.
> 
> When im at home I usually stream from my desktop, so streaming is really important.
> 
> For streaming, Im using 2 Variants, 1 for steamgames, 1 for non\_steamgames:
> 
> **1-- Moonlight -> Sunshine -> Playnite (esp. for non steam games, other launchers like epic, gamepass, gog, ...)**
> 
> set up moonlight and Sunshine (with sunshine\_utils [https://github.com/foxy82/sunshine\_utils](https://github.com/foxy82/sunshine_utils) - to set my Desktop PC to 1920x1200 // 16:10) - ,installed playnite on my desktop, connected the launchers I have (Epic, Gamepass, Steam, gog) to playnite, created an application in sunshine to start playniteFullscreenapp.exe with DO-COMMAND <path to sunshine utils>\\resolution\_change.exe --height 1200 --width 1920 (to set my desktop to 16:10) and UNDO <path to sunshine utils>\\resolution\_change.exe --height 1440 --width 2560 (to set it back to the native resolution)
> 
> This works well, no hazzle, no black bars on the deck (at least for games supporting 16:10) and all the precious non-steam games are streamable perfectly fine.
> 
> **2-- Moondeck (for steam games) -> Moonlight -> Sunshine**
> 
> nearly the same for moondeck, the above method for resolution change (DO / UNDO) is applied to the self-created application for moondeck in sunshine, because in my case, if moondeck (or moondeckbuddy) sets my Desktop resolution to 1200x800 in always sets the refreshrate to 60hz (on my 144hz panel), I dont know why, I dont know how to change that. I disabled all automatic resolution changes in the moondeck settings so sunshine can do the work. Also you have to install Moondeckbuddy on your desktop and pair it with moondeck.
> 
> After that, you only have to click on the moondeck icon in the steam-decks game-overview to start streaming. Its very easy, very comfortable.
> 
> My Problem with moondeck is that I dont really know how it works. It somehow creates a "non steam game" / Shortcut for the game you're running, so somehow the steam integrated-remoteplay/streaming doesnt work for this game anymore (after clearing the shortcuts in Moondeck settings it works again). I know thats a bit counterintuitive, but in some games steams Remote play still works really well and is great to use.
> 
> It also enables steams Big picture Mode on my desktop-PC for "reasons" and is not closing it when exiting a game. After some research, you can edit the settings.json file next to the moondeckbuddy launcher to disable steambigpicture.
> 
> Moondeck itself is great, I can WOL my desktop and even can send it to sleep, restart it or shutit down, that alone is a must install for me.

> **ExistingEagle3328** • [9 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kimzuco/) • 2024-01-19
> 
> 1000 easy to do steps, so your steam deck can do what it already does.

> **ElderlyKratos** • [4 points](https://reddit.com/r/SteamDeck/comments/19ahzxq/comment/kil74o9/) • 2024-01-19
> 
> Moon deck doesn't work for non steam games, does it?