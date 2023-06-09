---
title: Mount a physical drive inside a Oracle VirtualBox Machine
author: silviu
type: post
date: 2010-07-27T09:17:47+00:00
url: /2010/07/27/mount-a-physical-drive-inside-a-oracle-virtualbox-machine/
categories:
  - old
tags:
  - temp_on
  - virtualbox
  - virtualization

---
Sometimes I have to check drives under their native operating system. Recently I wanted to access a ntfs partition directly under Windows running inside a virtual machine. Here's how to (easily) do it:


```bash
VBoxManage internalcommands createrawvmdk -filename ./ntfs_test.vmdk -rawdisk /dev/sdb -register</p> 

VirtualBox Command Line Management Interface Version 1.5.4

(C) 2005-2007 innotek GmbH
All rights reserved.

RAW host disk access VMDK file ./ntfs_test.vmdk created successfully.
```

What this means? Well:

We create a virtual machine disk (vmdk) pointing to you physical drive. <strong>/dev/sdb</strong> in our case, be sure to point to yours. <strong>-register</strong> if set will tell VirtualBox to already register the drive inside your <em>Virtual Media Manager.</em>

<strong>DANGER: </strong>the disk will be fully available to the guest operating system. This means full access - so any command you use is definitive. Should you delete, partition or format the drive this will happen exactly as if you have booted the guest operating sytem directly.
