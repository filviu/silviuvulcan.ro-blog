---
title: Shrink (resize) a LVM volume
author: silviu
type: post
date: 2011-05-17T09:11:18+00:00
url: /2011/05/17/shrink-resize-a-lvm-volume/
dsq_thread_id:
  - 327260447
categories:
  - old
tags:
  - linux
  - logical
  - lvm
  - resize
  - root
  - server
  - shrink
  - temp_on
  - ubuntu
  - volume

---
I found a lot of resources on resizing LVM volumes or volume groups. But resources on shrinking were a little scarce and I couldn&#8217;t easily find a simple step by step method listed, so here you go. Please note that the volume you intend to shrink must be unmounted. If you want to resize the root partition (because like me you didn&#8217;t noticed that the ubuntu server installer will alocate the full 500Gb HDD for the root) you will have to boot off a LiveCD. I used the ubuntu server install cd and booted in _Rescue Mode_.

After it boots press ALT+F2 to move to a console.

Let&#8217;s see first the layout:  
[ccNe_bash]  
lvdisplay  
[/ccNe_bash]  
Let&#8217;s try and see if the volumes are there:  
[ccNe_bash]  
ls /dev/vgname/volume  
[/ccNe_bash]  
On the first try I got nothing so we must enable them:  
[cceN_bash]  
vgchange -a y  
ls /dev/vgname/volume  
[/cceN_bash]  
Yep, they are all there.

Before anything else we need to check the volume for errors (resize2fs will not work if you don&#8217;t)  
[ccNe_bash]  
e2fsck -f /dev/vgname/volume  
[/ccNe_bash]  
After that we resize the filesystem:  
[ccNe_bash]  
resize2fs /dev/vgname/volume 15G  
[/ccNe_bash]  
**Note that if you resize the volume to a size smaller than the file system it will trim it (the file system) and probably destroy it**  
Above, I reduced the filesystem from 453 to 15gb. That is a 438Gb gain.  Just to be on the safe side I will resize the volume only with 435Gb (leaving play room of over 3Gb which is plenty enough, 1Gb should be sufficient).

_E.g. if you want your final size to be 15Gb than resize the fs to 14Gb, shrink the logical volume to 15Gb and then grow the file system back._  
[ccNe_bash]  
lvreduce -L -435G /dev/vgname/volume  
[/ccNe_bash]  
Let&#8217;s put whatever was left for safety to use (grow back the file system to the full volume size):  
[ccNe_bash]  
resize2fs /dev/vgname/volume  
[/ccNe_bash]  
Just to be on the safe side let&#8217;s check the filesystem for errors.  
[ccNe_bash]  
e2fsck -f /dev/vgname/volume  
[/ccNe_bash]  
If you, like me, have resized the root than now you should reboot, otherwise simply mount back the volume and enjoy the free space by creating new volumes.

<span style="color: #ff0000"><strong>Remember! I resized a test environment, which didn&#8217;t matter if it went away. If you resize a production system (or anything else with useful data on it) remeber to BACKUP!</strong></span>