---
layout: post
title: "Burning an ISO to a USB stick on Mac OSX"
date: 2013-03-12 21:53
comments: true
categories: [iso, burn, usb, linux, install, crunchbang]
---

My kids have dropped my 10+ year old Sony Vaio laptop one final time, so it's time to find another old laptop (they'll do it again) &amp; put a fresh Operating System (OS) on it.  For the past 5 years the old Vaio had been running [CrunchBang](http://crunchbang.org/) OS (Statler build) with no problems at all.  It's fast & minimalist, totally perfect for little monkeys (& significant others).  Another big plus is the kids have previously downloaded a few viruses, but as CrunchBang is a variant of the [Linux](https://en.wikipedia.org/wiki/Linux) OS the viruses have had no effect as they are targeting Windows OS.   Linux has it's security right, with superuser's only allowed to install software that may do any real damage...  You can still get viruses for Linux, but there aren't as many for sure.

{% youtube yX8yrOAjfKM %}

Anyway you probably knew all that already?  Last time I installed CrunchBang I burned a CD, but I wanted to get down with the cool kids and use one of those new fangled USB sticks to install it.  Plus wowzas, the latest Waldorf build has an ISO that is bigger than a CD now!  CrunchBang have some [documentation](http://crunchbang.org/forums/viewtopic.php?id=23267) on how to burn to USB, but from another Linux box.  So I thought I'd [put down what you need to do](http://imgs.xkcd.com/comics/tech_support_cheat_sheet.png) if you're on OSX.  My google-fu failed me when I tried to look for “Burn a ISO image to USB stick on OSX”

Firstly it's **really important** to find out which device your USB stick is.

Side story: I once worked for a company whose multi-million pound [virtualization system](https://en.wikipedia.org/wiki/VMware_ESX) was wiped clean by one of our "IT staff" deciding it was a good idea to format their USB stick from the actual virtualisation machine.  It had devastating effect; they also discovered that some important services were _not_ being backed up!  Oh my, the :shit: really hit the fan that day!!  So please be careful.

{% youtube T2QApwtE8zQ %}

If they'd just followed these following steps that should not have happened.

### Find the correct device first:

*     Make sure the USB stick is removed from your machine


*     Open a terminal

*     Type ```diskutil list```


      You then should see something similar to this:

```
/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI                         209.7 MB   disk0s1
   2:                  Apple_HFS Macintosh HD            429.9 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
   4:       Microsoft Basic Data BOOTCAMP                69.3 GB    disk0s4
```

  This is the disk (&amp; partitions) that I do *not* want to touch!!!  You may have more than one?

*     now put the USB stick in and run ```diskutil list``` again

```
/dev/disk0
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *500.1 GB   disk0
   1:                        EFI                         209.7 MB   disk0s1
   2:                  Apple_HFS Macintosh HD            429.9 GB   disk0s2
   3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
   4:       Microsoft Basic Data BOOTCAMP                69.3 GB    disk0s4
/dev/disk1
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:     FDisk_partition_scheme                        *8.1 GB     disk1
   1:                 DOS_FAT_32 NO NAME                 8.1 GB     disk1s1
```


Now you can see there is a new device.  That's the USB stick!!!  ```/dev/disk1```  (You should also probably check that it's big enough to take the ISO you want to burn.)

###  Create a DMG

*      Before you can burn to USB you have to convert the ISO to a dmg file:

  ```hdiutil convert -format UDRW -o crunchbang crunchbang-11-20130119-i686.iso```

    Where crunchbang-11-20130119-i686.iso is the current download from CrunchBang, this could of course be *any* ISO.

###   Burn to the USB stick

*     When that's complete run ```sudo dd if=crunchbang.dmg of=/dev/diskN bs=8192```

      where the /dev/diskN is the USB disk we discovered earlier. In my case /dev/disk1.  I'll repeat it once more, incase you are stupid and you made it this far ;)

      => **!!!!please make sure you reference the correct USB disk!!!!** <==

      From now on I'll reference it as diskN so you don't copy and paste, and then access the wrong disk! :)

*     If you get the error message: dd: /dev/diskN: Resource busy

      Then run: ```diskutil unmount diskN```  and rerun the last command.

### Winning!

*     When complete you should see something like:

```
100224+0 records in
100224+0 records out
821035008 bytes transferred in 132.323860 secs (6204739 bytes/sec)
```

*     Finally, to safely eject the usb stick run ```diskutil eject /dev/diskN```

Now you have a USB stick (that you may boot from if the ISO is meant to be booted)!

{% youtube FjvFW71zJeM %}

BTW. You may have to [change your BIOS setting](https://duckduckgo.com/?q=how+to+get+into+bios+) to boot from the USB stick?






