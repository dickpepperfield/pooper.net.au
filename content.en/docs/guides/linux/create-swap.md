---
title: Create Swap
Description: Create Swap
date: 2024-12-16
tags: 
  - linux
  - guide
categories: guide
---

# Create Swap

In this guide, we'll create a swap file on CentOS.

This guide will provide steps on the quickest way to create a swap file on CentOS, should work on both CentOS 7, 8 and Stream. Before proceeding with this tutorial, check if your CentOS installation already has swap enabled by typing:

```bash
sudo swapon --show
```

1. Create file
```bash
sudo dd if=/dev/zero of=/swapfile bs=1024 count=1048576
```

2. Lock to root perms
```bash
sudo chmod 600 /swapfile
```

3. Make Swap and enable it
```bash
sudo mkswap /swapfile
sudo swapon /swapfile
```

4. Persist on boot
```bash
sudo vi /etc/fstab

/swapfile swap swap defaults 0 0
```

5. Change swappiness
```bash
vi /etc/sysctl.conf 
vm.swappiness=10
```