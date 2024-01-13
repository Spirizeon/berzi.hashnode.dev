---
title: "How to build special USBs"
datePublished: Thu Mar 16 2023 05:51:44 GMT+0000 (Coordinated Universal Time)
cuid: clfap1j7g000109l6gouv3hqm
slug: how-to-build-special-usbs
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1678945866968/84af3865-ef6c-4f62-8850-9d0360bbe2c6.png
tags: hacking, usb, badusb, hacking-tools

---

# BadUSBs

*A badUSB is type which corrupts the user's computer on plugging in*

## Components

* USB stick
    
* Generic script (that does anything)
    
* [Autorun](https://usb-autorun-creator.en.softonic.com/)
    

## Script

* can be written in any language
    
* must manipulate the file system
    
* functionality depends on extension and operating system
    

## Autorun

do note that the Autorun software must

* direct to the path of the USB folder
    
* direct to the script that is to be executed Also, the script needs to be saved inside the autorun folder before hand.
    

## Warning

Only make one for joke purposes, or in mild pranks.

# Bootable USBs

*A bootable USB is a kind that is used to store and load operating systems into devices*

## Components

* USB stick
    
* USB formatter (Like Rufus or Balena Etcher)
    
* Another computer
    
* Operating system image
    

First of all, we download an ISO file (which stands for International Standard Organisation), which is an image of the operating system that we are about to load onto the computer.

Then we take a USB stick, empty all its storage out, then download a formatter that will convert our USB from an ordinary flash memory to a bootable one. This means that it will project the option to choose another OS inside the USB in the BIOS.

For that we use Balena Etcher since it is the fastest and easiest way for one to format a flash stick. We choose the ISO image file, then we wait for the program to finish formatting. Now that the USB has become bootable, all its older content has been wiped (which was why we had to empty it out before hand to protect and backup any previous information stored on it). We restart the device with the USB plugged in. It will now show us the option to either load the new OS from it into the device, boot up the default OS.

In some cases, when we boot up the OS from the USB, there lies the problem of persistence, of whether we want to store the entire OS on the pendrive itself, or load it up on an existing secondary storage device on the computer.

### LiveUSBs

These are a subset of bootable USBs that do not store anything on the secondary storage device. Plug in, do your work, plug out. Nothing affects the existing data on the secondary storage device. But it is quite dangerous too, if the drives don't have proper encryption, you can access their data through the USB, alter, or even delete them! However, the good purpose on liveUSBs lie in this darkness itself. you can even backup your data through it incase your existing operating systems get corrupted and don't boot up.

On booting any version or variant of operating system, there is usually a demo version of that OS before actually installing it on the drives on the system. That is the OS running a live environment, which is temporary and running with the aid of the USB. There are many linux version that are specialised to fit and run on a USB. Like puppy linux, slax, and peppermint OS.