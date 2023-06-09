---
title: Prevent update-grub from finding LVM based virtual machines
author: silviu
type: post
date: 2014-12-09T09:12:54+00:00
url: /2014/12/09/prevent-update-grub-from-finding-lvm-based-virtual-machines/
categories:
  - old
tags:
  - debian
  - temp_on
  - xen

---
I'm running a debian based XEN box to host various virtual machines. Lately I've been having an issue when running `update-grub`. All the partitions for the virtual machines are found and added to grub:

```bash
# update-grub2
[...]
Found Debian GNU/Linux (7.7) on /dev/mapper/vg0-vm01-disk
Found Debian GNU/Linux (7.7) on /dev/mapper/vg0-vm02-disk
Found Slackware Linux (Slackware 14.1) on /dev/mapper/vg0-vm03-disk
[...]
```

It's not a big issue as the xen kernel is still default but it's annoying. Turns out the fix is simple enough, you have to add one line to _/etc/default/grub_ like this:

```bash
GRUB_DISABLE_OS_PROBER=true
```

After that re-run `update-grub`.