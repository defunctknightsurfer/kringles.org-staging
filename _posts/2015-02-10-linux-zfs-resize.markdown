---
layout: post
title:  "Linux ZFS & resizing single disk pool"
date:   2015-02-10 09:15:28
categories: linux zfs vmware
---
In a virutal enviorment I have found that I still like a lot of the features of zfs, but I do not end the RAID functionaily.  With that I had the need to expand a single disk zpool due to space issues.  In the past, we simply just added a second disk creating a RAID 0.  But I knew there was a better way.  ZFS on Linux does support resizing or autoexpand on a single disk zpool.  To do this, do the following steps.


1. Create or Set your zpool with autoextend on (it defaults to off)

        zpool set autoexpand=on tank

2. Via your Virtual Host tools, extend the disk in question to the size you need.
3. Now on your VM, get the disk name in your zpool

        zpool status

4. Run parted on that disk to resize the partition.

        parted /dev/sdb

5. Now simply use resizepart and it will default to the max 

        (parted) resizepart                                                       
        Partition number? 1                                                       
        End?  [X.XGB]?                                                           
        (parted) quit   

6. Now that you completed that, you need to just tell the zpool to expand.  You can do this online by running the following command.

        zpool online -e tank sdb

7. You should now notice that your partition is now larger

        df -h

