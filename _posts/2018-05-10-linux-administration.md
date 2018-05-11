---
inFeed: true
description: 'Image: Tux, the mascot of Linux drawn by  Larry Ewing in 1996.'
dateModified: '2018-05-11T05:35:51.809Z'
datePublished: '2018-05-11T05:35:52.718Z'
title: Linux Administration
author: []
publisher: {}
via: {}
hasPage: true
sourcePath: _posts/2018-05-10-linux-administration.md
starred: false
datePublishedOriginal: '2018-05-11T05:33:30.479Z'
url: linux-administration/index.html
_type: Article

---
# Linux Administration
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/d9563fee-0d55-4aa6-9b62-f2cfc50f93f3.png)

Image: Tux, the mascot of Linux drawn by Larry Ewing in 1996\.
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/d162116a-b12c-4000-864d-56c107afb419.png)

Screenfetch of Ubuntu logo drawn by the terminal.

### What this post covers

* Lesson 1: Linux Boot Process **CHECK**
* Lesson 2: System messages and logging **CHECK**
* Lesson 3: disk and file system management CHECK
* Lesson 4: managing users and groups CHECK
* Lesson 5: Linux networking concepts and applications CHECK
* Lesson 6: Process and job management
* Lesson 7: file and directory permission
* Lesson 8: installing managing software
* Lesson 9: shell scripting

---

## Lesson 1\. Linux Boot process

### Bios

* Basic Input/output System
* Special firmware
  * 1st piece of software that is run
* OS independent
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

### Boot Loaders

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
  * Ring Buffer is a data structure that at is always the same size
    * Once buffer is full, old messages are discard
  * Contains messages from the Linux kernel
  * _**\# dmesg**_
    * see contents/messages of the ring buffer
  * _**/var/log/dmesg**_
    * messages stored on disk
    * to check those messages that fly by on bootup

### Runlevels

* Runlevels determine what processes to start on boot up
  * 0 Shuts down the system
  * 1, S,s Single user mode. Used for maintenance
  * 2 Multi-user mode with graphic interface (Debian/Ubuntu)
  * 3 Multi-user text mode (RedHat/CentOS)
  * 4 Undefined
  * 5 Multi-user mode with graphical interface (Redhat/CentOS)
  * Reboot

* Init
  * _**/etc/inittab**_:
  * _**\# id:3:initdefault**_:
    * Example of setting run level 3 to the default run level
    * Phased out by systemd

* Systemd
  * Uses targets instead of runlevel
    * Find list of targets
      * _**\# cd /lib/systemd/system**_
      * symlinks to the real targets being used
      * _**\# ls -l runlevel5.target (shows the symlink)**_
  * _**\# systemctl set-default graphical.target**_
    * change default run level to graphical.target
    * _**\#systemctl set-default multi-user.target**_
      * Multi user target, see run levels
  * Change run level/target using init system
    * _**\# telinit 5**_ (change to run level 5)
  * Change run level/target using Systemd
    * _**\# systemctl isolate graphical.target**_

### Rebooting

* There is a run level / target for rebooting or you can use the reboot or shutdown commands
* _**\# telinit 6**_ (reboot with init)
* _**\# systemctl isolate reboot.target**_ (reboot with systemd)
* _**\# reboot**_
* Syntax
  * _**\# shutdown \[options\] time \[message\]**_
  * _**\# shutdown -r 15:30 "rebooting at 15:30!"**_
  * _**\# shutdown -r +5 "rebooting in 5 minutes!"**_
  * _**\# shutdown -r now**_

### Power Off

* _**\#telinit 0 **_(init system)
* _**\#systemctl isolate poweroff.target **_(systemd system)
* _**\#poweroff**_

### Summary Lesson 1

* Linux Boot Process
* BIOS is to perform basic hardware checks and to start the bootloader from a bootable device
* Two most common bootloaders LILO and Grub
* Bootloader is to start operating system, files are stored in /boot directory
* Initial ram disk or initrd is temporary file system that is loaded into memory, main job is to mount the file system where OS is stored
* Linux Kernel is VMLinux or VMLinuz
* View Messages in Kernel Ring Buffer using dmesg command or find them in /var/log/demesg
* Runlevels and Systemd's equivalent concept known as targets
* telinit change run level for init
* systemctl change run level for systemd
* shutdown, reboot, poweroff commands

---

## Linux Boot Process Demo

Press F2 to enter BIOS configuration utility

* List of bootable devices
  * change the order
  * executes boot loader
* exit bios

GRUB Menu
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/691d9091-8d8c-4639-ac11-423c9198272a.png)

* Bios executes BootLoader from first bootable device it can find
* Select operating system
  * Press 'e' key to inspect the kernel
  * Line that starts with linux tells the bootloader which kernel to use
    * Anything that appears after the kernel is an argument on boot
    * hit escape
  * hit enter to boot up

He is using CentOS Linux 7 (Core)

* on the CentOS systems the terminal begins with \#

1. login through root
2. runs \#reboot command to pass args to kernel
3. presses e on menu item in GRUB then takes away the Quiet
  * ctrl x to boot with that config
  * now we see more messages on boot
4. logs back into message
5. _\# **dmesg**_ (shows contents of kernel ring buffer aka the message on startup)
  * _**\#dmesg | less**_
    * piping the output to a pager called less
    * number is bracket represent time in seconds since boot
      * run _**\# dmesg -T | less**_to see it in human readable time
  * ring buffer will fill up so to see all the messages since boot
6. _**\# cat /var/log/dmesg**_
  * run | less on this as well
7. _**\# cd /boot**_
  * _**ls**_
  * see notes on files in /boot
  * _**ls grub2**_ (using grub2 in this example)
  * _**\# cd /etc/inittab**_
    * init used to control run levels, but we are now using systemd..
  * _**\# systemctl get-default**_
    * We see that it is set on multi-user.target
    * _**\# systemctl set-default graphical.target**_
  * _**\# systemctl isolate graphical.target**_
    * booting with graphical user interface

---

## Lesson 2: System Log Standard

* syslog standard
* facilities and severities
* syslog servers
* logging rules
* where logs are stored
* how to generate your own log messages
* rotating log files

### The Syslog Standard

* Aids in the processing of messages
* Allows logging to be centrally controlled
* Uses facilities and severiies to categorize messages
* ### Facilities

* What type of program that they originated from (kern, mail etc)
* Each has number and keyword associated with it

* Number Keyword Description
* 0 kern kernel messages
* 1 user user-level messages
* 2 mail mail system
* 3 daemon system daemons
* 4 auth security/authorization messages
* 5 syslog messages generated by syslogd
* 6 lpr line printer subsystem
* 7 news network news subsystem
* 8 uucp UUCP subsystem
* 9 clock daemon
* 10 authpriv security/authorization messages
* LinuxTrainingAcademy.comNumber Keyword Description
* 11 ftp FTP daemon
* 12 - NTP subsystem
* 13 - log audit
* 14 - log alert
* 15 cron clock daemon
* 16 local0 local use 0 (local0)
* 16 local1 local use 0 (local1)
* 16 local2 local use 0 (local2)
* 16 local3 local use 0 (local3)
* ...
* 23 local7
* local use 7 (local7)

List of Severities Code, Keyword, and Description

* 0 Emergency emerg (panic) System is unusable
* 1 Alert alert Action must be taken immediately
* 2 Critical crit Critical conditions
* 3 Error err (error) Error conditions
* 4 Warning warning (warn) Warning conditions
* 5 Notice notice Normal but significant condition
* 6 Info info Informational messages

### Syslog Servers

* Process syslog messages based on rules
* _**\# syslogd**_
* _**\# rsyslog **_(most common)
* _**\# syslog-ng**_

Rsyslog

* _**\#/etc/rsyslog.conf:**_
  * Main config file
  * _**$IncludeConfig /etc/rsyslog.d/\*.conf**_
    * Include addition config files
    * Include all conf files in that end in .conf that also exist in the rsyslog.d directory

Logging Rules

* Selector field
  * FACILITY.SEVERITY
    * format
  * mail.\*
    * wildcards are supported
  * mail
    * equivalent to mail.\*
  * FACILITY.none
    * match no messages to facility
  * FACILITY\_1.SEVERITY; FACILITY\_2.SEVERITY
    * match multipel sev

* Action field
  * Determines how a message is processed
* Example: matches messages that have the facility of mail and any severity
  * _**mail.\* /var/log/mail.log**_
  * writes to var/log/mail.log

Caching vs Non-caching

* Caching is used if the path starts with ahyphen
  * _**mail.info -/var/log/mail.info**_
  * If path starts with a minus sign so it does not have to perform a sync operation for each log message
* You may lose some messages during a systemcrash if you are using caching mode.
* Using caching mode can improve I/Operformance.

Example Logging Rules

* _**mail.info -/var/log/mail.info**_
* _**mail.warn -/var/log/mail.warn**_
* _**mail.err /var/log/mail.err**_
  * notice how this one is not using a cache but the more important messages are

* _**auth,authpriv.\* /var/log/auth.log**_
  * ensures all messages from auth & authpriv facilities are in log
* _**\*.\*;auth.none,authpriv.none -/var/log/syslog**_
  * writes all messages except auth and authprive
* _**\*.info;mail.none;authpriv.none;cron.none /var/log/messages**_
  * write all except mail, authprive, cron

Logger Command

* Generate syslog messages
  * test any config changes youve made to system logger or generate log messages from own shell scripts
* logger \[options\] message
  * Options:
    * -p FACILITY.SEVERITY
      * it will default to user.notice if not specified
    * -t TAG
* ex:
  * _**$ logger -p mail.info -t mailtest "Test."**_
    * generate message with mail facilitity with severity of info
  * _**$ sudo tail -1 /var/log/mail.log**_
    * _**Apr 4 14:33:16 linuxsvr mailtest: Test.**_
    * You can see that it made its way to the proper log file

Logrotate Command

* /etc/logrotate.conf:
  * config file of this command
* Rotate compress move or email log files
* include /etc/logrotate.d
  * found in .conf file
  * Tells it to read config files located in etc/logrotate.d
* Example logrotate.conf located at /etc/logrotate.d/rsyslog
  * weekly
    * updated weekly
  * rotate 4
    * delete messages older than 4 weeks
  * create
    * ensure new empty log file is created after rotated
  * compressed
  * include /etc/logrotate.d
* Example logrotate.conf located at /etc/logrotate.d/rsyslog

    /var/log/debug
    /var/log/messages
    {
      rotate 4 #rotate file by count times before removing them
      weekly
      missingok #ingore missing logs
      notifempty #dont rotate file if empty
      compress #comporess rotates log files
      sharedscripts
      postrotate #using binsh
      	reload rsyslog >/dev/null 2>&1 || true
      endscript
    }

* Test the logrotate configuration
  * _**\# logrotate -fv /etc/logrotate.conf**_
    * -f says force rotate
    * -v enable verbose logging

### Summary

* The syslog standard: assigns facilites and serverity to each message
* Facilities and severities
* Syslog servers: employ use of logging rules to determine what action to perform on given message
* Logging rules: typically just store message in log file
* How to generate your own log messages: logger utility
* Using logrotate: automatically prune system logs

---

## Lesson 3: Disk and File System Management

In this lesson

* Partitions
* MBR
* GPT
* Mount points
* fdisk

### Partitions

* Disks can be divided into parts, called partitions.
* Partitions allow you to separate data.
* Partitioning schemes
  * 1) OS, 2) Application, 3) User, 4) Swap
  * 1) OS, 2) User home directories
  * As a system administrator, you decide.
* Can protect the overall system.
* Keep users from creating outages by using a home directory partition.

### Partition schemes

MBR

* Master Boot Record
* Can only address 2 TB of disk space
* Being phased out by GPT
  * GPT= GUID Partition Table
* 4 Primary Partitions
* Extended partitions allow you to create
* logical partitions

GPT

* GPT = GUID Partition Table
* GUID = Global Unique Identifier
* Replacing the MBR partitioning scheme
* Part of UEFI
* UEFI = Unified Extensible Firmware Interface
* UEFI is replacing BIOS
* Supports up to 128 partitions
* Supports up to 9.4 ZB disk sizes
* Not supported by older operating systems
* May require newer or special tools

Mount Point

* A directory used to access the data on a partition
* / (slash) is always a mount point
* /home
  * /home/jason is on the partition mounted on /home
* /export/home
  * /export/home/jason

Mounting over existing data

* _**mkdir /home/sarah**_
* _**mount /dev/sdb2 /home**_
* \* You will not be able to see /home/sarah now.
* _**umount /home**_
* \* You can now see /home/sarah again.
* You can Mount Points on Mount Points

_**fdisk**_ (partitioning tool)

* _**fdik /path/to/device**_
* alternative: gdisk, parted

### Summary

* Partitions
* Partition tables
  * MBR
  * GPT
* Mount points: directories used to access data on partition
* fdisk: create partitions

### Create Partitions with fdisk

* _**fdisk -l**_
  * displays list of devices
  * can see if there is partitions
  * we saw one called dev/sdb
* _**fdisk /dev/sdb**_
  * _**m **_for help
  * _**n **_create partition
  * Creating a swap partition
  * _**p** to print device info_
  * _**g **to create GPT partition_

### Creating, Mounting, Unmounting File systems

* Prepare swap space for use
* FIle system Table
* Disk UUIDs and labels

* ext4 = Most common Extended File system
* other file systems for specific needs
* _**mkfs -t TYPE DEVICE**_
  * _**mkfs -t ext3 /dev/sdb2**_
* _**mount DEVICE MOUNT\_POINT**_
  * _**mount /dev/sdb3 /opt**_ // mounting sdb3 on opt
* _**mount **_command with no args to see what is currently mounted
  * also see virtual file systems
* _**df -h**_
  * reports file system usages
* To make a mount permanent (doesnt persist between reboots)
  * add entry in _**etc/fstab **_file
* _**umout DEVICE\_OR\_MOUNT\_POINT**_
  * umount /opt
  * umount /dev/sdb3

Preparing Swap Space

* You create swap area and then enable it, dont mount
* _**mkswap /dev/sdb1**_
  * set up swap space
* _**swapon /dev/sdb1**_
  * enable
* _**swapon -s**_
  * see swap devices

_**/etc/fstab**_

* Controls what devices get mounted and where on boot
* Device File: Device Mount Point, File system type, options, dump fsck order
* Ex: /etc/fstab file

\# device mount point FS options dump fsck

* /dev/sda2 / xfs defaults 0 1
* /dev/sda1 swap swap defaults 0 0

_**lsblk -f**_

* display UUID of devices and labels

_**blkid**_

* display device UUID

Labeling a file system

* _**e2label /dev/sdb3 opt**_
  * for ext systems
  * labels ex: root or opt

Summary

* mkfs: make file systems
* mount
* df: view disk usage of mounted disk
* umount: unmount
* mkswap: prepare swap space
* swapon: enable swap space
* /etc/fstab file to mount devices using path, uuid, or label
* viewing UUID and label

---

## Lesson 3b: Logical Volume Manager

Why use LVM?

* Create file systems that extend to multiple storage devices
* Expand or shrink file systems in real time while the data is still available
* Easily migrate data from on storage device to another while the data is online
* Convenient device naming
* Stripe data across two or more disks which allows parallel read
* LVM can mirror data
* Snapshots = consistent backups

### Layers of Abstractions
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/660e6a8b-32de-422e-b2ec-eb499684e167.png)

* PV: do not have to be physical but made available to linux
  * block storage devices like harddrives
* VG: Pool of storage
  * PVs backed by
* LV: file systems are created on top of these
  * usually extended

### Creating Logical Volumes

* Create Physical Volume
* Create Volume Group from PV
* Create Logical Group From VG

    $ su - switch to root user
      password:
    [root~]# lvmdiskscan #what devices are available
    # lsblk #find out about block devices
    # lsblk -p # find out which device is mounted where, we see on mounted on / and see full paths with -p
    # df -h #shows disk space usage in readable form -h
    # fdisk -l #see storage attached to linux system
      
    # pvcreate /dev/sdb #initializes disk and create physical disk
    # pvs #see list of physical devices
    
    # vgcreate vg_app /dev/sdb #vgcreate NAME LOCATION OF PHYSICAL DISK
      
    # vgs # see phsyical volumes
    # pvs #now shows us that we are in a volume group
      
    # lvcreate -L 20G -n lv_data vg_app #create logical volume and size -L, -n name
    # lvs #view logical volumes
    # lvdisplay #different view of lvs
      
    # mkfs -t ext4 /dev/vg_app/lv_data #file system on lv
    # mkdir /data #create directory
    # mount /dev/vg_app/lv_data /data #mounting logical volume
    
    #df -h /data #now we can see that/data has 20G available because of the size of LV
    
    # lvcreate -L 5G -n lv_app vg_app  #creating another lv to actually store files of example
    # mkfs -t ext4 /dev/vg_app/lv_app #put file system on there
    # mkdir /app #creating mount point
    # vi /etc/fstab #add it here so it gets mounted at boot time
    # mount /app #now it will read the /etc/fstab 
      
    #df -h /app #we see it mounte
      
    # ls -l /dev/mapper/vg_app-lv_app
      ls -l /dev/vg_app/lv_app #this is how you access the data
      
    # lvdisplay #see the path of lv
    
    #vgs #see the volume group information to check available storage
    
    # lvcreate -L 25G -n lv_logs vg_app #we are trying to create another lv to store logs in our example, however it cannot be 25G
    # lvcreate -l 100%FREE -n lv_logs vg_app #using the rest of space of vg into lv
      
    # vgs #tells us that our volume group is completely allocated
    # lvmd
      
      
      Video Continues with Section 3, Lecture 11 on extending VGs and LGs

vi /etc/fstab

    /dev/sda1     /          ext4 defaults       0 0
    /dev/vg_app/lv_app  /app ext4 defaults 0 0#path to storage device
      

Summary

* pvcreate /dev/sdb
* vgcreate vg\_name /dev/sb \#configure vg
* lvcreate -L 10G -n lv\_name vg\_name
* mkfs -t ext4 /dev/vg\_name/lv\_name
* lvextend -L +10G -r /dev/vg\_name/lv\_name \#extend lv
* pvcreate /dev/sdc
* vgextend vg\_name /dev/sdc \#add more to VG
* lvcreate -m 1 -L 100G 0n lv\_name vg\_name \#mirror lvs
* lvremove /dev/vg\_name/lv\_name
* vgreduce vg\_name /dev/sdb
* vgremove vg\_name
* pvremove /dev/sdb

---

## Lesson 4: Managing Users and Groups

* How to manage users and groups
* Where user and group info lives
* How to add, delete and change users and groups

### Accounts have:

* Username (or login ID).
* UID (user ID). This is a unique number.
* Default group.
* Comments.
* Shell.
* Home directory location.

_**/etc/passwd **_file

* root:x:0:0:root:/root:/bin/bash
* The format of the /etc/passwd:
  * username:password:UID:GID:comments:home\_dir:shell
  * x means password stored in shadow file
* joe:x:1000:1000:Joe Henderson:/home/joe:/bin/bash
  * username:password:UID:GID:comments:home\_dir:shell
* _**$ ps -fu joehenderson**_ view account info
* Usernames
  * Less than 8 characters in length by
  * convention.
  * Case sensitive.
  * In all lowercase by convention.
  * Numbers are allowed in usernames.
  * Do not use special characters
* Passwords are stored in _**/etc/shadow**_
  * Encrypted password used to be stored in /etc/passwd.
  * /etc/passwd is readable by everyone.
  * Now, encrypted passwords are stored in /etc/shadow.
  * /etc/shadow is only readable by root.
  * Prevents users trying to crack passwords.
* UIDS
  * The root account is always UID 0\.
  * UIDs are unique numbers.
  * System accounts have UIDs < 1000\.
    * Configured in /etc/login.defs
* GID (group ID)
  * The GID listed in the /etc/passwd for is the default group for an account.
  * New files belong to a user's default group.
  * Users can switch groups by using the newgrp command.
* Comment Field
  * Typically contains the user's full name.
  * In the case of a system or application account, it often contains what the account is used for.
  * May contain additional information like a phone number.
  * Also called the GECOS field.
* Home Directory
  * Upon login the user is placed in their home directory.
  * If that directory doesn't exist, they are placed in "/".
* Shell
  * The shell will be executed when a user logs in.
  * A list of available shells are in /etc/shells.
  * The shell doesn't have to be a shell.
  * To prevent interactive use of an account, use
  * /usr/sbin/nologin or /bin/false as the shell.
  * Shells can be command line applications
  * Could force users into a menu based access that only allows users certain actions
* _**/etc/shadow**_
  * root:$6$9g1IC8AYzqoZP21:16502:0:99999:7:::
  * username:encryptedpassword:\#ofdayssincejan11970sincepasschange:\#ofdaytillavailablepasschange:\#ofdaysuntilpassmustbechanged(99999meanuserdoesntneedtobechanged):\#ofdaystowarnuserpassisexp:\#ofdayspassexpireduntilcountisdisabled:\#ofdaysaccdisabled

### Create an Account

* _**useradd**_
  * useradd\[options\]username
  * _**-c**_ "comment"
  * _**-m**_ home directory
  * _**-s/shell/path**_ the path the user's shell
  * ex: useradd --c "Grant Stewart" --m --s /bin/bash grant
    * \# passwd grant
    * _**\# tail -1 /etc/passwd**_
      * grant:x:1000:1000:Grant Stewart:/home/grant:/bin/bash
    * **\# tail -1 /etc/shadow**
      * grant:$6$iDDsgsPYtR8c2Uc.:16507:0:99999:7:::
  * _**-g **_GROUP
  * _**-G**_ GROUP1,GROUPN
  * ex: \# useradd --c "Apache Web Server User" --d /opt/apache --r --s /usr/sbin/nologin apache
    * _**\# tail -1 /etc/passwd**_
    * apache:x:999:999:Apache Web Server User:/opt/apache:/usr/sbin/nologin
  * _**-d**_ specify a directory (we didnt use -m)
  * _**--s/usr/sbin/nologin apache**_ user is not allowd to login
  * _**-r**_ create a system account
  * _**-u**_ specify UID
  * ex: \# useradd --c "MySQL Server" --d /opt/mysql -u 97 --s /usr/sbin/nologin mysql
  * \# tail -1 /etc/passwd
    * mysql:x:97:1003:MySQL Server: /opt/mysql:/usr/sbin/nologin

* /etc/skel
  * used with -m to copy shell config files to home directory

* _**userdel\[-r\] username**_
  * Example of deleting user but leaving home files intact
  * _**-r**_removes files as well

    # ls /home
    eharris grant
    # userdel eharris
    # ls /home
    eharris grant
    # userdel -r grant
    # ls /home
    eharris

* _**usermod**_
  * usermod \[ options \] username
    * -c "COMMENT"
    * -g GROUP
    * -G GROUP1,GROUPN
    * -s /shell/path

* _**/etc/group**_
* _**groups \[username\]**_
* _**groupadd \[ options \] group\_name**_
* _**groupmod \[options\] group\_name**_

Summary

●

Account information is stored in:

* /etc/passwd and /etc/shadow

Accounts have the following attributes:

* username
* UID
* GID (default group)
* Comment
* home dire

* Create accounts with **useradd**.
* Delete accounts with **userdel**.
* Modify accounts with **usermod**

* Group information is stored in /etc/group.
* Create groups with **groupadd**.
* Delete groups with **groupdel**.
* Modify groups with **groupmod**.
* To view group memberships use groups

---

## Lesson 5: Networking

* TCP/IP
  * see network+
  * TCP = control data exchange
  * IP = sends data between devices
* Classful networks
  * A1.0-127 allowing 16,777,216 hosts
  * B 128-191.255 allows 65,535
  * C 192.0.0 allows 255 hosts per network
* Subnet masks
  * see Network+
* Broadcast addresses
  * see Network+
  * always maxed out last octet
* CIDR
  * classles interdomain routing
  * subnets inside networks
* Private address space
  * Non routable private address space
  * aka RFC1918 addressed
* Determining your IP address
  * _**ip address**_
  * ip addr
  * ip a
  * ip address show _or _ip a s
* ip and ifconfig utilities
  * ipconfig
* hostnames
  * host is device connected to a network hostname corresponds to IP address
* DNS and name resolution
  * FQDN = fully qualified domain name
  * TLD aka top level domain
    * .com, .net, .org, etc.
  * Domains
    * webprod01.mycompany.com
  * below (to the left of) TLD
    * sub-domain
    * below (to the left of) the domain
    * webprod01.ny.us.mycompany.com
  * _**$ hostname**_
  * _**$ uname -n**_
  * _**$ hostname -f **_(display FQDN)
  * Setting the hostname
    * _**\# hostname webprod01**_
    * _**\# echo 'webprod01' \> /etc/hostname**_
    * _**\# vi /etc/sysconfig/network**_
      * make it persist between reboots
      * HOSTNAME=webprod0
  * _**host**_
    * look up IP address of DNS name or IP address
* /etc/hosts
  * local file containing list of ip addresses and host name
  * overrides so you could force people to use address you want or so they dont have to type in an ip
* /etc/nsswitch.conf
  * controls the order in which look ups are performed
  * can query before DNS
* Network ports
  * When a service starts it binds itself to a port.
  * Ports 1 - 1,023 are well-known ports.
  * 22 - SSH
  * 25 - SMTP
  * 80 - HTTP
  * 143 - IMAP
  * 389 - LDAP
  * 443 - HTTPS
  * /etc/services
    * maps port names to port numbers
* DHCP
  * DHCP servers assign IP address to DHCPclients
    * IP Address
    * netmask
    * gateway
    * DNS servers
  * Each IP is "leased" from the pool of IPaddresses the DHCP server manages.
    * The lease expiration time is configurable on the DHCP server. (1hr, 1day, 1 week, etc.)
  * ifconfig -a _or_ ip link
  * /etc/network/interfaces to assign a static ip
* Static IP addresses
  * Manually assigning an IP adress
  * ip address add IP\[/NETMASK\] dev NETWORK\_DEVICE
  * ip address add 10.11.12.13 dev eth0
  * ip address add 10.11.12.13/255.255.225.0 dev eth0
  * ip link set eth0 up
* ifup / ifdown
  * commands to test config changes to network interfaces
* GUI / TUI tools
  * RedHat
    * nmtui
    * system-config-network
  * SUSE
    * YaST
  * Ubuntu
    * No official tool available

### Network Troubleshooting
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/9dee4aa0-3981-4ae9-bfac-9079d6a32834.png)

* ping
  * ping HOST
  * ping -c COUNT HOST
* traceroute / tracepath
  * attempts to translate ip address to dns names
    * -n gets ride of this
  * sends packets the 3 packets at each hop along the way
    * issue exists if one of the packets at one of the hops takes a long time to get back
* netstat
  * -n Display numerical addresses and ports.
  * -i Displays a list of network interfaces.
  * -r Display the PID and program used.
  * -p Display listening sockets. (netstat -nlp)
  * -l Limit the output to TCP (netstat -ntlp)
  * -t Limit the output to UDP (netstat
  * -u -nulp
  * _**sudo netstat -ntlp**_
    * Displays the local programs that are listening on ports!
* tcpdump
  * Older Packet sniffing tool
  * -n Display numerical addresses and ports.
  * -A Display ASCII (text) output.
  * -v Verbose mode. Produce more output.
  * -vvv Even more verbose output.
* telnet
  * telnet is deprecated because of ssh
  * telent HOST\_OR\_IP PORT\_NUMBER
  * Tests for port connectivity
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/ae7151fb-bbdc-404b-9106-9f0daaf74b87.png)