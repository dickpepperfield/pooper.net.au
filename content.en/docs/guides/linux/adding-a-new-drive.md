---
title: Adding a New Drive
Description: Adding a New Drive
date: 2024-12-16
tags: 
  - linux
  - guide
categories: guide
---

# Adding a New Drive

In this guide, we'll add a new disk, and format it for use. This guide makes assumptions about drive lettering and paths, ensure you're running things where you want to.

------

1. Determine drive name and logical size.
```bash
fdisk -l
```

2. Partition drive using fdisk
```bash
fdisk /dev/sdc

# Common commands

n – Create partition
p – print partition table
d – delete a partition
q – exit without saving the changes
w – write the changes and exit.
```

3. Create Partition using whole Block Device, defaults are fine

![](/images/4e337b43-3617-4f0d-9231-848273f628a9.png)

4. Determine partition name
```bash
lsblk
```

5. Make the file system
```bash
mkfs.xfs /dev/sdc1
```

6. Mount the drive, a few improvements related to random read in the form of noatime
```bash
mount -t xfs -o noatime,nodiratime /dev/sdc1 /mnt/block/rust/
```

7. Verify that the filesystem is mounted

8. To persists across reboots, ensure /etc/fstab updated with he following line.
```bash
/dev/sdc1 /mnt/block/rust/ xfs defaults,noatime,nodiratime 0 0
```


