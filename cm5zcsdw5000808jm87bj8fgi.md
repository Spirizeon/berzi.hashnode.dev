---
title: "Hacking your way back into Windows"
datePublished: Thu Jan 16 2025 13:15:17 GMT+0000 (Coordinated Universal Time)
cuid: cm5zcsdw5000808jm87bj8fgi
slug: hacking-your-way-back-into-windows
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1767961650511/d310f74b-da76-4618-b570-bb3848ad13b7.jpeg

---

This article is more like an emergency guide I made for both the readers and myself. The intended audience are those people who wanna install a copy of Windows 10/11 on a fresh SSD/HDD or switch from Linux to Windows in a Dual boot/Clean install configuration.

## This wasn’t Hacking, until it was…

Why “Hacking”? That’s coz Microsoft loves to make things complicated! Traditional ISO flashes like Balena etcher, Popsicle nowdays won’t support making a windows bootable USB. Hence you’re left with usually two most efficient methods to create a bootable USB:

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">An ISO, also called the “image file” is a file with an extension of “.iso” that contains the installation wizard to install the specific OS into your system</div>
</div>

1. Install Ventoy, flash it into the USB, drag and drop your windows ISO into the USB drive… OR
    
2. Create a Windows VM (which is thankfully easy to setup), install Rufus, give the VM access to the USB drive, then flash the ISO into the drive directly through Rufus.
    

Now we got our USB drive, what next? Drivers! Why? Because Windows won’t detect your drive without them, and without detection, you won’t be able to install your OS! I’ll target two kinds of drivers: one from Intel, and one from AMD.

## Drivers driving us insane

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737032398450/f51c6303-a5ec-4049-b07a-7c5e0901b0c9.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1737032468051/e3314013-6f76-4378-8094-acb13c0eae9f.png align="center")

For either of these, install the respective `.exe` file, on a Windows VM. This will create the driver files and save them in your system, organize them inside a folder and store them in a flash drive.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">a VM or a Virtual Machine is an OS that can run over your main OS. These can be managed through hypervisors like VirtualBox and VMWare Pro (Try Googling).</div>
</div>

## Double USB ninja technique!!!

Now you gotta go ninja mode. Plug the first USB drive made bootable with Windows 10, set the boot priority to make sure you boot into the USB drive. After the installation wizard starts, select “Custom Install”, then see if any drives are being detected, if not, click “Load drivers”. You might come across this screen…

![Troubleshooting windows installation error “No device drivers were found.”  | by Syed Hasan | Medium](https://miro.medium.com/v2/resize:fit:1400/0*4_SGhxNySIful9_5.png align="left")

Now plug in your second flash drive containing the drivers, click “browse”, and then recurse through the files of that flash drive until you reach the “VMD” folder inside the driver files (that’s for Intel’s case at least). Select it, load and you’ll be able to see the drives now! Continue with your installation, and you should smoothly be able to setup Windows 10 from scratch now. (Also, please update your system clock and install Windows Updates to make sure you get the required firmware, security patches and other drivers)