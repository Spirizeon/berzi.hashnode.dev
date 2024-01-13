---
title: "Portable linux"
datePublished: Thu Mar 16 2023 05:57:02 GMT+0000 (Coordinated Universal Time)
cuid: clfap8cap000409l69el9asyy
slug: portable-linux
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678948108107/ec7d283d-e882-49e7-97db-c40a4c21d6ee.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678948139423/7048e750-ed5c-47de-9684-3ac3e9490924.jpeg
tags: linux, termux

---

## Why carry linux?

Here are some reasons you'd like to read:

* Allows you to SSH into your servers for any work/editing
    
* Gives you an instant environment for coding
    
* You can self-host your code on your phone and carry it (the server) everywhere!
    

### 1\. Install Termux from [Fdroid](https://f-droid.org/en/packages/com.termux/) or [Play Store](https://play.google.com/store/apps/details?id=com.termux&hl=en_US&gl=US)

Termux is an Android terminal emulator and Linux environment app that works directly with no rooting or setup required.

### 2\. Install Linux!

You can either work your own way around it through termux or simply copy paste the script below into your termux app

```bash
pkg install proot-distro
proot-distro install debian 
proot-distro login debian
```

This will install the proot-distro utility that manages installations of the Linux distributions in Termux. Lastly, we're choosing debian here (any other available distro works too).