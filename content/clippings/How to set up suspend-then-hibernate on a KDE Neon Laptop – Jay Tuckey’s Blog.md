---
title: "How to set up suspend-then-hibernate on a KDE Neon Laptop – Jay Tuckey’s Blog"
source: "https://jaytuckey.name/2023/02/07/how-to-set-up-suspend-then-hibernate-on-a-kde-neon-laptop/"
author:
  - "[[Jay Tuckey]]"
published:
created: 2025-10-09
description:
tags:
  - "clippings"
---
`suspend-then-hibernate` is a neat feature in systemd that allows a computer to suspend (aka sleep) for a period of time, then wake up, and hibernate.

To configure this required a few steps on KDE Neon (also tested on Kubuntu 23.10), though:

## Configure Hibernate

To configure hibernate, you need to have a swap partition that is as large as your system’s memory. It’s best to have it on a separate partition, not a swapfile, as it’s much easier to configure that way. Here’s my setup:

![](https://jaytuckey.name/wp-content/uploads/2023/02/image.png)

```
free -m # this will show you free memory
```

You need to make sure the partition auto-mounts as swap (add to `/etc/fstab`), then also need to add a `resume` parameter to the kernel parameters in the `/etc/default/grub` file.

![](https://jaytuckey.name/wp-content/uploads/2023/02/image-1.png)

```
lsblk | grep -i swap  # list block devices, and search for lines with the word "swap"

blkid /dev/<swap partition>  # get the UUID of the swap partition

grep <uuid> /etc/fstab  # This will find the line to mount the swap automatically

grep <uuid> /etc/default/grub  # This will find the line to add the "resume=" kernel parameter
```

Once this is reconfigured, you also need to rebuild the initramfs and grub config:

```
sudo update-grub
sudo update-initramfs -k all -c
```

Then, reboot, and make sure the swap is mounted (you can use the `swapon` command to see). Once confirmed, use the command `sudo systemctl hibernate` to test hiberation and restoring from hibernation.

## Enable hibernation in Ubuntu / KDE Neon

In KDE Neon, hibernation is disabled by default using polkit. To enable it, comment out the lines in this file, needs to be edited with sudo like this:  
`sudo vim /var/lib/polkit-1/localauthority/10-vendor.d/com.ubuntu.desktop.pkla`  
(found at [https://phabricator.kde.org/D16425](https://phabricator.kde.org/D16425))

```
[Disable hibernate by default in upower]
Identity=unix-user:*
Action=org.freedesktop.upower.hibernate
#ResultActive=no  # commented this line
ResultActive=yes  # and replaced with this line

[Disable hibernate by default in logind]
Identity=unix-user:*
Action=org.freedesktop.login1.hibernate;org.freedesktop.login1.handle-hibernate-key;org.freedesktop.login1;org.freedesktop.login1.hibernate-multiple-sessions;org.freedesktop.login1.hibernate-ignore-inhibit
#ResultActive=no  # commented this line
ResultActive=yes  # and replaced with this line
```

Reboot, and check that you have a “Hibernate” button in the menu. Test it works.

Edit `sudo vim /etc/systemd/sleep.conf` and uncomment the line “HibernateDelaySec=…” and set to a value you want. For testing I use 1m, otherwise something like 45m is good.

Then, go into system settings to the “Energy Saving” section, and look for the option “While asleep, hibernate after a period of inactivity” and turn it on:

![](https://jaytuckey.name/wp-content/uploads/2023/02/image-2-1024x765.png)