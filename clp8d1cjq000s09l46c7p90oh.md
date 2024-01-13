---
title: "Dual booting Linux with Windows"
datePublished: Tue Nov 21 2023 13:17:11 GMT+0000 (Coordinated Universal Time)
cuid: clp8d1cjq000s09l46c7p90oh
slug: dblww
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700573018746/eab7a299-0e9a-4dfc-ba9f-a29e4c357276.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1700573090045/2f2f4b8b-c422-4600-beb8-32da76f81cef.png

---

### Partitioning the drives

Lets assume our system has a single secondary storage device. So we will split the entire storage into two separate and isolated chunks. One will have windows and other will have Linux.

On windows, go to start &gt; search "format partitions..." and select the most similar sounding option from the list, if you got the right one, a window will pop up showing all the partitions and mounted drives in the system visible to windows.

select the drive which you want to install linux on, here, we want to store it in the C:/ drive, so we will right click on that &gt; select "shrink volume".

In the wizard window, we will make a space of 100GBs, since the space is in MBs, the input would be `100000` &gt; click enter.

now we will have chunk of the C:/ drive as unallocated space for Linux.

### Flashing the USB drive

For the most hassle-free process of flashing our USB stick with the operating system ISO (the OS image or installer file in layman's terms), we will use [Balena Etcher](https://etcher.balena.io/) (or [Rufus](https://rufus.ie/en/))

After installing it, we will plug our USB stick. Make sure to empty it out as it will be formatted when making it Bootable (make it visible to the BIOS but unfit for storing regular files).

Select and download your preferred operating system ISO of your choice, it can be ubuntu, pop os, or even arch! Select your USB drive and the ISO file from Balena's wizard window and start formatting!

### Boot into Linux

Now restart, your computer. Our aim is to set the flash-drive's boot priority to the top so that it boots up before Windows. Open up the BIOS settings (the shortcut key is to be pressed at the time of system startup when the manufacturer's logo is showing) through the BIOS shortcut key (it usually varies between brands so look on the internet for your laptop's model). Go to an option that sounds similar to "boot configuration", and do as intended in the first statement of this paragraph.

Turn off secure boot if the Linux variant's documentation says so, then apply changes and exit. You will now boot into Linux.

### Configuring partition file systems

After configuring a few things in the installation wizard (if it does not open by default, click on the desktop icon where it says "install")

*let the installer do the work if it is insisting on it*... *but do make sure you know what it's doing*.

you may come across an option called "edit partitions", click that. you will find a particular option with 100 GiBs or approximately near to it in one of the options, that is the space we made beforehand.

Now we shrink and split that volume of 100GBs into a

* 4GBs chunk for the `swap` chunk with the `linux swap` or `swap` filesystem, this will house the `/swap` directory.
    
* 2GBs for the `boot` partition chunk with the `FAT32` filesystem, this will house the `/root` directory.
    
* the rest for the `ext4` filesystem, this will house the `/home` directory.
    

Now, click next and wait for the installation to finish.

### Last few things...

At last, the system will reboot for the changes to take place, now we can remove the USB when its rebooting. Welcome to Linux!