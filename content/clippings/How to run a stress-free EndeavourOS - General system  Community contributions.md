---
title: "How to run a stress-free EndeavourOS - General system / Community contributions"
source: "https://forum.endeavouros.com/t/how-to-run-a-stress-free-endeavouros/49769"
author:
  - "[[OctoTV]]"
published: 2024-01-29
created: 2025-08-16
description: "im completely new to Linux and i was wondering are there any apps/things i should install to make my life easier"
tags:
  - "clippings"
---
## How to run a stress-free EndeavourOS

[General system](https://forum.endeavouros.com/c/general-system/5) [Community contributions](https://forum.endeavouros.com/c/general-system/community-contributions/39)

[dalto](https://forum.endeavouros.com/u/dalto)

I have spent a lot of time over the last 8 years helping people fix their broken systems and seeing people constantly describe how much trouble it is to keep their Arch-based systems running. Meanwhile, even though I run many systems with different configs, I never actually have these problems myself.<sup>1</sup> I have helped people with so many obscure issues that if I ever did have issues with systems failing after an update I could fix them myself without too much trouble in most cases. However, I don’t have to. I don’t have those issues on my normal systems.<sup>2</sup> Is this because I am some kind of Linux techno-ninja? No. I am not doing anything special or using any special skills or deep knowledge. I use my day to day systems the same as everyone else does. In fact, I generally have more complicated setups that should be *more* prone to breakage.

Lately I have been thinking about why this is and that led me to start thinking about all the things that cause breakage or cause frustration for other people. I think there are some things people do that make it more difficult and/or stressful than it needs to be. I made a list of these things, hoping that it would help people who want a system that “just works” without having to worry about it overly.

First, I will warn you that some of these things go against what other guides and tutorials will recommend you do. Someone is bound to pop in and say I do “insert thing here” and have never had a problem. Maybe that is luck, maybe there is some other factor. These are based on my personal experiences and my experience helping others fix problems. Second, if you have a good level of expertise or prioritize fun over stability don’t follow these. Instead, do what you enjoy. These aren’t must do items that will cause a failure if you don’t do them. They are things that increase your chances of not having a failure in the first place.

In order of importance:

1. **Use the LTS kernel** - No seriously. Unless you have a specific reason not to use the LTS kernel, use it. It is very common for new kernels to have issues with certain hardware or configurations. The LTS kernel protects you from 90% of these issues.
2. **Uninstall your update notifier** - I often see people switching distros due to the frequency of updates and the stress caused by it. Arch streams constant updates in, but you don’t need to update all the time. There is no good reason to use an update notifier on Arch. There will almost always be updates. It is OK to ignore them. Personally, I update about twice per month. I would recommend updating at least once per month but otherwise whenever you feel like it. You can install `arch-audit-gtk` to ensure you are not missing any security updates.
3. **Install only a single DE/WM** - You only need one, trust me. Most of us go through a phase of having multiple DEs/WMs. It can be fun at first to try out a bunch and switch between them. However, most of us also learn three things in that process. Having more than one causes lots of little inconsistencies since they tend to step on each other in small ways, it actually isn’t a great way to test DEs because you are introducing breakage that otherwise wouldn’t be there and, lastly, you never really know if the issues you see are caused by a bug or the fact that you have/had multiple DEs installed. Use a VM or a second machine to test new DEs. Also, you don’t need a “backup DE”.
4. **Let your updates finish before rebooting** - A decent amount of the issues we see people having with their systems is caused by not letting updates finish. There are processes that run at the end of the of the update process that are critical to the boot process.
5. **Make sure your root partition doesn’t become completely full** - This one is pretty obvious. Don’t let your root partition fill up. If it happens during an update, it can cause some serious havoc that can be hard to recover from
6. **Use a simple partition layout** - Want to know a great way to avoid your partitions from filling up? Have less of them. Just have a single partition with `/` and an EFI partition. Add a swap partition if you want/need one. Splitting your free space between partitions just makes storage management more complicated.
7. **Use a simple system configuration** - The simpler your system is, the less prone it is to breakage. This is general advice but one example would be using btrfs, grub and snapshot booting. People often do this so they can more easily roll back from failures. However, this setup adds complexity and increases your chance of having failures in the first place. Complexity is a balancing act. Keep it as simple as you can to achieve your goals.
8. **Don’t re-use `/home`** - People will often tell you to have a separate partition for `/home`. IMO, this is terrible advice. You should never share `/home` between distros. Even with the same distro, it typically doesn’t make sense to re-use it. If there is some problem that causes you to reinstall, the issue is just as likely to be in `/home` as outside of it. If you want to preserve or share your personal data, instead, create a partition or subvolume that contains your user data and then mount or symlink the data to `~/Documents`, `~/Videos`, `~/Picture`, etc.
9. **Have some amount of swap** - If you completely run out of memory, your system hard crashes. This is bad. Having some swap will decrease the chance of this happening. It doesn’t matter if it is zram, a swapfile or a swap partition. Just have some swap.
10. **Don’t reset or hard power off your system** - It causes filesystem corruption and other issues. Don’t so it. Be sure to [enable Sysrq](https://forum.endeavouros.com/t/tip-enable-magic-sysrq-key-reisub/7576) which allows you to use REISUB if your system freezes.
11. **Don’t install packages you don’t use** - The more packages you have, the more complicated updates become. This is especially true for AUR packages that may be tied to specific library versions creating problematic dependencies. To be clear, I am not advocating for maniacally removing packages. Just install the software you actually use and remove the stuff you don’t.
12. **Don’t use 3rd party repositories** - In addition to all the [risks associated with these repos](https://forum.endeavouros.com/t/faq-the-dangers-of-using-3rd-party-repos/11803/1), they also make updates more complicated and are often the cause of issues.
13. **Don’t use `*-git` packages without a reason** - These packages usually pull from the latest source code in a repo. In addition to the fact that this means more frequent updates, this code is usually unreleased and often untested. There are of course, exceptions. Sometimes things like theming will only have a git package because the theme owners don’t actually do releases.
14. **Use a minimal maintenance routine** - People often ask how I maintain my system. I do three things. When using advanced filesystems, I setup a scheduled job automate those tasks on a monthly basis. I remove orphans a few times per year. I update the system a couple of times per month. That is it. I don’t clean my package cache, I don’t merge pacnew files. I don’t prune the logs or anything else. To be clear, I am not saying never to do any of these things. You may need to do some of them(Like pruning your package cache if you are low on disk space). However, too many people break their systems trying to maintain them. Keep it minimal.
15. **Don’t use bleachbit and friends** - This is an extreme version of the above point. These tools often “over clean” and break your system or applications.
16. **Read the questions pacman asks you** - Don’t just hit the enter button and accept the default choice. Especially when you are installing or removing software. Often those questions are important.
17. **Don’t multi-boot** - Yes, it can be fun to run a bunch of different OSes but it also makes things more complicated and more prone to breakage.
18. **If you multi-boot, don’t use os-prober** - `os-prober` is imperfect. If you multi-boot, either use systemd-boot, grub with manual stanzas or refind with manual stanzas. When using grub or refind, I recommend chain-loading. It may be an extra click or an extra couple of seconds at boot but it is 100% reliable with all UEFI installs.
19. **Don’t follow advice you don’t understand** - Typing commands a random stranger on the internet gives you is a bad idea. Typing commands from a random Reddit post that may or may not be related to your issue is even worse. If you don’t understand what a command does, ask someone to explain it.
20. **Use common, mainstream hardware** - Sometimes, we don’t have the luxury of choosing hardware. However, when you do have the choice, use common mainstream hardware that is well supported in Linux. Avoid newly released hardware when possible.

Bonus - **Maintain backups** - This doesn’t make your system more reliable. However, having backups can be the difference between a really bad day and a minor bump in the road. Always have backups.

The reality is that most of this stuff is true for any distro. With a few small exceptions, you can treat EOS/Arch like a non-rolling distro if you want to.

That being said, an Arch-based distro isn’t for everyone and there are some times when you just shouldn’t use one

- **You are extremely bandwidth constrained** - Arch, being a fast moving distro will see a lot more long-term bandwidth usage than an LTS distro. If this is a concern, something based on Debian stable, Ubuntu LTS or RedHat is probably a better choice
- **You update less than once per month** - If you can’t update at least once every month-ish, you may be better off with a non-rolling distro.
- **The primary user of the device wants a completely hands-off automated experience** - If the person using the OS doesn’t want to ever see the terminal or think about the minor questions that pop-up during an update or software install you are probably better off with something that supports that use-case better. Solus, PopOS or Linux Mint for example.
- **You need commercial support for your applications** - Very few commercial applications officially support Arch. Often, this is because it is pretty hard to test and certify something that is constantly changing.
- **You prefer your applications to not change** - If you hate when applications change and new features mess up the menu layout you are used to, you are better off with a distro that doesn’t get new application versions as often

<sup>1 - Do I occasionally have minor issues introduced by getting the latest software? Yes. But these are usually annoyances, not system breaking issues.</sup>  
<sup>2 - I do a lot of development and testing so I often create expected breakage that I need to fix. However, that is in VMs where I am deliberately doing those things.</sup>

[thefrog](https://forum.endeavouros.com/u/thefrog) Dev ISO tester

I would add

Making sure that USB devices have finished their task before removing them.

[Kresimir](https://forum.endeavouros.com/u/kresimir) frog

All good advice, there is not a single thing in the OP I disagree with, except maybe the order of importance.

I think the first thing should always be having a good backup: at the very minimum multiple copies of all important files on external drives. If you have that, a broken system, either due to hardware or software failure, is just an annoyance. Even if you never have a software problem, all hardware will eventually fail, so one has to expect that and be prepared.

[GolDNenex](https://forum.endeavouros.com/u/goldnenex)

I would also add “Don’t buy nvidia gpu”

[Zircon34](https://forum.endeavouros.com/u/zircon34)

one thing that I might add, and also stressed in the past. Systems can break on updates and result in black screen at startup. Commonly resulting from a graphics driver update. More than often problems with Nvidia.

no need to panic and re-install the whole system or switch distros. Keep an Endeavour OS usb as one can chroot into the system to fix that. The forum can walk less experienced users through it. Essentially one can boot into the system, fix packages, update/downgrade packages, while all user files etc. still work and exist in the background.

[Kresimir](https://forum.endeavouros.com/u/kresimir) frog

Absolutely, if you are buying a new computer, get AMD graphics.

Unfortunately, most of the time, you’re stuck with what you already have and have to make the best of it.

[ExDebianuser](https://forum.endeavouros.com/u/exdebianuser)

Yes—i do most of this…I will say that I multi-boot - to run Winblows when I “really” need to & my backup install of EOS. I keep a complete backup install as a reference as I like to mess around with my system from time-to-time…it’s easy to have an unmodified install to reference back to when you muck up…

I also run fairly up to date hardware…mostly to see what breaks & why. Of course, I LIKE the fast-rolling nature —I used to work with Debian-Unstable & Sid…so not seeing at least 20~50 updates when I look is…not fun. I know this makes me an “outlier”----- but I LIKE solving problems with software & hardware.

I also ALWAYS question the what & why…keeps my mind active & I always learn a new thing or two…

[drunkenvicar](https://forum.endeavouros.com/u/drunkenvicar) Regular

damn, pretty brilliiant write-up but #1 surprised me the most. Never did much research re: Current vs. LTS. What is all that about? Most problems with ‘hardware or configurations’ are solved by the next update usually (although I know not for everyone).

\[Like you, Dalto, I strangely don’t have the problems I see posts about although I am pre-dispositioned to accidentally obliterate my install on reckless occasion…\]

[kabe](https://forum.endeavouros.com/u/kabe)

Great guide and I quite agree - as a newbie, you constantly hear people going on about how Arch-based distros are a hassle to maintain but I have had far fewer issues with Endeavor than I did with (supposedly) more “stable” distros, like Fedora.

Ever since switching to the LTS kernel 6 months ago and upgrading my system maybe once a week, I haven’t needed to fix anything significant at all.

[ExDebianuser](https://forum.endeavouros.com/u/exdebianuser)

I’m still cheering for the Intel stuff…after the initial “teething” --running with my Arc A750 has been very smooth…can’t wait until the next release—the BattleMage cards are supposed to be very good.

[dalto](https://forum.endeavouros.com/u/dalto)

Right, but if you use LTS they never happen in the first place. Because LTS is basically an older kernel version so the teething issues with new kernels doesn’t occur there as easily.

[ExDebianuser](https://forum.endeavouros.com/u/exdebianuser)

I do have to admit to using git packages … but people need to THINK about WHY they are using a git…right now I’m running into problems with OpenRGB & some pesky RAM…I just updated to a rather new-ish Asus ROG Gaming-H & the RGB on the RAM (G-Skill DDR5-6400) is “locking-up” after a couple of hours of use…One of the developers & I are trying to find out why…

The first thing to try was OpenRGB-git (version.91) to see if the support for this new hardware was better (it’s not).

[ArchieLinux](https://forum.endeavouros.com/u/archielinux)

[@dalto](https://forum.endeavouros.com/u/dalto) Outstanding post.

Having faced few issues using EOS/Arch the past year+, I have had my butt saved via Vorta/Borg + Timeshift several times. Hence I, too, like [@Kresimir](https://forum.endeavouros.com/u/kresimir) would put that atop this list.

FWIW, I seem to be following many (if not most) of the listed suggestions, except I do update frequently. But having three separate EOS installations running at a time lets me sandbox updates to ensure things are okay.

One additional suggestion: Check the forum for alerts/warnings before updating. I could’ve saved myself some grief on a few occasions. But the rescue team on this forum is so prompt and helpful, perhaps it allows me to drive a little recklessly

[fbodymechanic](https://forum.endeavouros.com/u/fbodymechanic)

Sounds like a whole lot of my first rule in my update guide. Don’t break your own computer.

+1 for the lts. I know I’ve said the same thing countless times. Unless you need latest, lts is hands down the better option.

[JKMooney](https://forum.endeavouros.com/u/jkmooney)

LTS is an older kernel with the latest security patches in place. The vast majority of people really don’t need the “latest available” kernel. If you really must, you should also install the LTS kernel as a backup just in case it does go “wonky” on you.

[smokey](https://forum.endeavouros.com/u/smokey)

Great guide, very similar to the rules I have for myself with next to no issues on the 3 computers I have used it on (including 1 with a NVIDIA GPU)

[ajaychat3](https://forum.endeavouros.com/u/ajaychat3)

[@dalto](https://forum.endeavouros.com/u/dalto). Perfect advice. You are rocking.

[ricklinux](https://forum.endeavouros.com/u/ricklinux)

The guide is great advice. Myself i never use an lts kernel. My feeling is I’m on an Arch based OS for a reason. I want the latest kernel and the latest software because I’m using newer hardware. It’s also hardware that all works on linux. I don’t have many issues but occasionally they pop up.

[Nomad](https://forum.endeavouros.com/u/nomad)

Great post. This should be pinned.

[ExDebianuser](https://forum.endeavouros.com/u/exdebianuser)

I agree with the post saying that this should be pinned…Great Topic dalto!