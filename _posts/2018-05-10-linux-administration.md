---
inFeed: true
description: ''
dateModified: '2018-05-10T17:56:05.769Z'
datePublished: '2018-05-10T17:56:08.682Z'
title: Linux Administration
author: []
publisher: {}
via: {}
hasPage: true
starred: false
datePublishedOriginal: '2018-05-10T17:56:08.682Z'
sourcePath: _posts/2018-05-10-linux-administration.md
url: linux-administration/index.html
_type: Article

---
# Linux Administration

### What this post covers

* Linux Boot Process
* System messages and logging
* disk and filesystem managment
* managin users and groups
* Linux networking concepts and applications
* Process and job management
* file and directory merission
* installing managing software
* shell scripting

---

## Linux Boot process

### Bios

* Basic Input/output System
* Speical firmeware
  * 1st piece of software that is run
* OS indepent
  * Not unique to Linux OS
* Purpose: Find and Execute Boot Loader
* Performs POST
  * Power-On Self Test
  * Tests CPU, Memory, Storage Device
* Contains and Searches list of Bootable Devices
  * Hard Drives
  * USB Drives
  * DVD Drives
  * Boot Sequence or Search order can be changed
* ### Boot Loaders

* Usually GRUB Bootloader
  * Grand Unified Bootloader
* LILO
  * Old Linux Systems
  * Linux Loader
* Bootloaders start the OS
  * Can start with different options
  * Different OS

### initrd

* Initial RAM disk
* Temporary File System that is loaded into memory from disk
* Contains helpers and Modules (drivers) required to load the permanent OS file system
  * LVMV - Logical Volume manager Volume initrd image will contain the kernel modules required to mount that LV as the root file system

* Once initrd mounts root file system, its job is done and the computer is booted from the root file system

### The /boot Directory

* /boot
  * contains the files required to boot Linux
  * initrd
  * kernel
  * bootloader configuration

    Here is the listing of /boot directory for an Ubuntu system
      $ ls -f /boot
      abi-3.13.0.46-generic
      config-3.13.0-46-generic
      grub/
      initrs.img-3.13.0-46-generic //initial ram disk
      System.map-3.13.0-46-generic
      vmlinuz-3.13.0-46-generic  //this is the kernel typically named this or vmlinux (ending in z means its compressed)

### Linux Kernel

* Kernel Ring Buffer
  * Ring Buffer is a data structure that is always the same size
  * Contains messages from the Linux kernel
  * dmesg
  * /var/log/dmesg
  * ### Runlevels

*