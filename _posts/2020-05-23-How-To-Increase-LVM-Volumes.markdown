---
layout: post
title:  "How to increase LVM volume space"
date:   2020-06-21 16:01:00
categories: Linux
---

Procedures

1. Create new partition with fdisk
2. Create physical LVM partition: ex) pvcreate /dev/sdb1
3. Add physical LVM partition to volume group: ex) vgextend centos /dev/sdb1 (see pvscan for LVM groups[centos])
4. Check the available PE size: ex) pvdisplay /dev/sdb1
5. Extend LV volume: ex) lvextend -l +[PEsize] /dev/centos/home
6. Grow the filsystem size: ex) xfs_growfs /dev/centos/home