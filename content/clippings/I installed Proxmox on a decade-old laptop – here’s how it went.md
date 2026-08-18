---
title: "I installed Proxmox on a decade-old laptop – here’s how it went"
source: "https://www.xda-developers.com/i-installed-proxmox-on-a-decade-old-laptop/"
author:
  - "[[Ayush Pande]]"
published: 2025-06-29
created: 2025-09-21
description: "One man's trash is another man's home server... or is it?"
tags:
  - "clippings"
---
If you’ve been a member of the tech community for a while, chances are you’ve already got a spare rig that ended up gathering dust once you moved to a new system. I’ve got a couple of outdated systems, but my Lenovo G510 laptop from 2014 takes the crown as the oldest device in my house that’s still somewhat functional. After unearthing it from the recesses of my home lab last month, I tried [using it as my primary Home Assistant node](https://www.xda-developers.com/i-turned-my-old-laptop-into-a-dedicated-home-assistant-hub/). With the experiment being a huge success, I wanted to see if I could restore my obsolete computing companion to its former glory by arming it with [Proxmox](https://www.xda-developers.com/proxmox-guide/).

After all, Proxmox pairs well with most hardware, and unlike Harvester, it doesn’t require a war machine just to run a couple of virtual machines. Now that I’ve spent half a day tinkering with the laptop-based Proxmox setup, I have to admit that it’s actually quite usable – as long as I keep my expectations in check, that is.

## Initial preparations for the project

### Enabling virtualization and taking some safety precautions

![Enabling Intel VTX in BIOS](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-13.jpg?q=49&fit=crop&w=825&dpr=2)

Since Proxmox is designed to run full-fledged operating systems inside virtual environments, the platform needs virtualization enabled inside the BIOS. So, navigating my way to the BIOS and tracking down this option was the first step in this experiment. My preferred method of entering the BIOS was as simple as mashing the **F2** and **F10** keys when the laptop booted up.

Luckily, the Intel Virtualization Technology option wasn’t that hard to find, though I was unable to find a certain useful setting that could’ve elevated this project’s utility. I’m referring to the option that lets users set a charging limit for their laptop’s battery. While a laptop’s battery can serve as a neat alternative to a UPS, charging it for hours on end can cause it to swell up and eventually turn into a fire hazard.

![Removing the battery from an old laptop](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/home-assistant-old-laptop-10.jpg?q=49&fit=crop&w=825&dpr=2)

I had a similar situation when I tried installing Home Assistant on the laptop. A commenter mentioned that I could try capping the maximum charging limit using a smart plug, which is an ingenious solution to my conundrum. But since my backwater town doesn’t have any retailers that stock up on smart plugs, my only choice is to wait for Amazon to deliver one in a couple of days.

Until then, unmounting the battery seems like the best course of action. Unlike modern laptops and their borderline irreparable designs, my ancient laptop has a simple latching mechanism that lets me disconnect the battery in a matter of seconds!

## Installing Proxmox on the dinosaur laptop

### It wasn't all that difficult, to be honest

Now that I’d finished the preparations, it was time to set up my favorite virtualization platform on the laptop. To make things simple, I went the old-fashioned route of flashing the Proxmox ISO onto a USB drive using Balena Etcher and using it to boot into the installation wizard. With the bootable drive ready, I made another quick trip to the BIOS and set it as the device with the highest boot priority.

After another restart, the familiar Proxmox Installation Menu popped up, and I spent the next couple of minutes selecting the correct **Storage Drive**, **Timezone**, and **Account Settings**. However, I had to be extra cautious when configuring the **Network Settings**, as I wanted my Proxmox server to use the Ethernet port instead of the WLAN connection. With all the settings configured, I hit the **Install** button and waited for the aged machine to set up Proxmox. To my surprise, the process barely took a couple of minutes, and soon, the laptop displayed the IP address for accessing my newly-configured Proxmox machine.

## The old system couldn’t handle GUI distros

### Its low RAM is the main culprit

![Transferring an ISO file to Proxmox](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-3.jpg?q=49&fit=crop&w=825&dpr=2)

Considering the Lenovo G510 has a 2-core, 4-thread Intel i5-4200M processor, I was certain the CPU would be a huge bottleneck. But what I didn’t realize was that the 4GB DDR3 module in the laptop would be the bigger issue when running virtual machines – especially those featuring GUI distributions.

![Running Debian on Proxmox](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-4.jpg?q=49&fit=crop&w=825&dpr=2)

As a Debian fanboy, I wanted to gauge the dinosaur system’s performance when running the king of vanilla distros. After transferring a Debian ISO to the Proxmox server, I used it to create a VM featuring 2 v-cores (which are different from CPU cores) and 2GB of RAM. Unfortunately, the virtual machine took a couple of minutes to boot into the Desktop, and while it wasn’t completely unresponsive, the latency was a little too high for me.

What’s more, the laptop’s fans started whirring right after I started the virtual machine, and the sound they made could best be described as the wailings of a dying hyena. A quick look at the RAM utilization bar on the System tab revealed that the 4GB memory was inadequate to keep up with the combined processing brunt of Proxmox and the virtual machine.

## But LXCs and lightweight distros are fair game

### Turns out, the laptop doubles as a solid self-hosting rig

With the GUI virtual machine failing to live up to my expectations, I decided to switch my attention to CLI distributions. With [DietPi](https://www.xda-developers.com/dietpi-guide/) being my favorite lightweight distro, I deployed a VM using its x86 ISO. This time, the Lenovo G510 managed to pull its own weight, and even with the same 2 v-core and 2048 MB memory limit, DietPi ran surprisingly well on the machine.

However, virtual machines are just one-half of the equation, as Proxmox natively supports Linux Containers. For the uninitiated, LXCs are a lot less taxing on the hardware than VMs, making them perfect for my outdated laptop. I used the Proxmox VE Helper-Scripts repository to deploy a Cosmos LXC, which is a containerization platform that can run even more services.

![Deploying IT-Tools on Cosmos](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-10.jpg?q=49&fit=crop&w=825&dpr=2)

To my surprise, the laptop was able to run a dozen containers on Cosmos, including [Paperless-ngx](https://www.xda-developers.com/host-paperless-ngx-on-your-home-lab/), [Nextcloud](https://www.xda-developers.com/how-build-google-drive-alternative-nextcloud/), Grocy, [Calibre-Web](https://www.xda-developers.com/host-your-own-e-book-library-with-calibre-web/), and other must-have utilities. Simultaneously, I may add. Since CasaOS includes a larger selection of apps, I also deployed another LXC and tried deploying a couple more services using this container.

![Deploying a couple of containers on CasaOS](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-19-1.jpg?q=49&fit=crop&w=825&dpr=2)

For the final round of tests, I tried running a Debian LXC alongside the DietPi VM as well as the CasaOS and Cosmos containers. This caused the RAM to hit over 90% utilization, though shutting down the virtual machine freed up a lot of memory – precious RAM that I can use to run even more containers!

### So, can an outdated laptop serve as a Proxmox hub?

![Proxmox configured on an old laptop](https://static0.xdaimages.com/wordpress/wp-content/uploads/wm/2025/06/proxmox-old-laptop-2.jpg?q=49&fit=crop&w=825&dpr=2)

Unless you’re planning to run Windows 11 or Linux distros with desktop environments, you can reuse old systems as Proxmox environments. Lightweight CLI distributions work pretty well, and if I could lay my hands on 8GB DDR3 memory sticks, I’m certain my laptop could run at least one GUI-heavy virtual machine.

Assuming your electricity rates aren’t too high, building a Proxmox workstation specifically for LXCs is a great way to recycle old hardware and prevent it from turning into e-waste. Heck, there are even a couple of practical uses for this setup. If you’ve already got a home lab centered around Proxmox (or any other platform, for that matter), you could use an old system like mine to host [Uptime Kuma](https://www.xda-developers.com/uptime-kuma-guide/), Pi-hole, or other mission-critical services that you wouldn’t want to risk running on an experimental machine.