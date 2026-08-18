---
title: "Need help configuring hibernation - General system / Kernel, boot, graphics & hardware"
source: "https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402/2"
author:
  - "[[firefly]]"
published: 2024-03-12
created: 2025-10-09
description: "I’m trying to configure hibernation and looks like I overlooked something. It’s a standard EOS setup with systemd-boot, dracut and swap partition roughly the size of RAM. According to Arch Wiki, if it’s UEFI system and s…"
tags:
  - "clippings"
---
## Need help configuring hibernation

[General system](https://forum.endeavouros.com/c/general-system/5) [Kernel, boot, graphics & hardware](https://forum.endeavouros.com/c/general-system/kernel-boot-graphics-hardware/33)

[firefly](https://forum.endeavouros.com/u/firefly)

[Mar 2024](https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402 "Post date")

I’m trying to configure hibernation and looks like I overlooked something.

It’s a standard EOS setup with `systemd-boot`, `dracut` and swap partition roughly the size of RAM. According to Arch Wiki, if it’s UEFI system and `systemd` version >= 255, hibernation should be working without any explicit configuration, so my whole setup process was basically this:

- created `/etc/dracut.conf.d/resume.conf` containing:
```makefile
add_dracutmodules+=" resume "
```
- regenerated images with `sudo dracut-rebuild` and rebooted

`lsinitrd -m` shows `resume` module, yet hibernation still doesn’t work. With both lts and mainline kernels. Every time - it’s just like fresh boot.

Would really appreciate any ideas/suggestions as to where I should start looking in order to sort it out

```
~ ❯ lsinitrd -m
Image: /efi/5fc0f8f4b17443e1863b494bc5c40cab/6.6.21-1-lts/initrd: 61M
========================================================================
Early CPIO image
========================================================================
drwxr-xr-x   3 root     root            0 Mar 12 12:37 .
-rw-r--r--   1 root     root            2 Mar 12 12:37 early_cpio
drwxr-xr-x   3 root     root            0 Mar 12 12:37 kernel
drwxr-xr-x   3 root     root            0 Mar 12 12:37 kernel/x86
drwxr-xr-x   2 root     root            0 Mar 12 12:37 kernel/x86/microcode
-rw-r--r--   1 root     root        14336 Mar 12 12:37 kernel/x86/microcode/GenuineIntel.bin
========================================================================
Version: dracut-059

dracut modules:
systemd
systemd-initrd
i18n
kernel-modules
kernel-modules-extra
resume
rootfs-block
terminfo
udev-rules
dracut-systemd
usrmount
base
fs-lib
shutdown
========================================================================
~ ❯ lsinitrd /efi/5fc0f8f4b17443e1863b494bc5c40cab/6.6.21-1-lts/initrd | grep resume
resume
-rwxr-xr-x   1 root     root        26936 Mar  3 18:04 usr/lib/systemd/systemd-hibernate-resume
-rwxr-xr-x   1 root     root        26976 Mar  3 18:04 usr/lib/systemd/system-generators/systemd-hibernate-resume-generator
```

[pebcak](https://forum.endeavouros.com/u/pebcak)

[Mar 2024](https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402/2 "Post date")

There is an issue with the current version of dracut (059-6) which needs an additional line:

```makefile
install_items+=" /usr/lib/systemd/system/systemd-hibernate-resume.service "
```

in `/etc/dracut.conf.d/resume.conf`

This issue should be fixed in the next release of dracut, if I have understood the matter correctly.

Add the above line, rebuild the initrds and try.

[firefly](https://forum.endeavouros.com/u/firefly)

[Mar 2024](https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402/3 "Post date")

That was fast  
Thank you - looks like problem solved. Just to clarify: when `dracut` 060 will be available, I should remove that line?

Also, while searching through forums, stumbled upon this [thread](https://forum.endeavouros.com/t/laptop-not-resuming-from-hibernation/37237/31) and turns out in my case `cat /proc/cmdline` shows somewhat similar duplication:

```bash
~ ❯ cat /proc/cmdline
initrd=\5fc0f8f4b17443e1863b494bc5c40cab\6.6.21-1-lts\initrd nvme_load=YES rw root=UUID=f61831a8-a60d-4891-b1f3-bc95e3c04bae resume=UUID=f
e6d8d44-8993-4ce7-aba9-7a9e2f9ca20f rw root=UUID=f61831a8-a60d-4891-b1f3-bc95e3c04bae resume=UUID=fe6d8d44-8993-4ce7-aba9-7a9e2f9ca20f sys
temd.machine_id=5fc0f8f4b17443e1863b494bc5c40cab
```

Is it normal? Or should I manually edit it as well?

edit: perhaps [@dalto](https://forum.endeavouros.com/u/dalto) could also kindly chime in

[pebcak](https://forum.endeavouros.com/u/pebcak)

[Mar 2024](https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402/4 "Post date")

I believe when next upgrade to dracut is here, then that additional line would not be necessary.  
Perhaps you could check with the forum to make sure that things are as they should be.

Also, I would look into `/etc/kernel/cmdline`, edit it to only contain the line below (according to the post you linked too) and rebuild the initrds

```lua
nvme_load=YES rw root=UUID=f61831a8-a60d-4891-b1f3-bc95e3c04bae resume=UUID=f
e6d8d44-8993-4ce7-aba9-7a9e2f9ca20f
```

[dalto](https://forum.endeavouros.com/u/dalto)

[Mar 2024](https://forum.endeavouros.com/t/need-help-configuring-hibernation/52402/5 "Post date")

You can remove it after the next upgrade to dracut. It is has been patched already in the Arch package for 059 but they have not yet released the version with that patch.

If those are truly duplicates, that isn’t normal and you should remove them. I do think there was a bug in an older version of the installer that created those dups. We fixed that quite some time ago but if your installation is older, it may be left over from that.

  

### Want to read more? Browse other topics in Kernel, boot, graphics & hardware or view latest topics.

[Powered by Discourse](https://discourse.org/powered-by)