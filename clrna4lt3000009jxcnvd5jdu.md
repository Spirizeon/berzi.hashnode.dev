---
title: "ZySec: Day #16"
datePublished: Sun Jan 21 2024 09:11:42 GMT+0000 (Coordinated Universal Time)
cuid: clrna4lt3000009jxcnvd5jdu
slug: zysec-day-16
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1705827084794/1b99b1ad-0077-4eb8-a465-c4ca9c240166.png

---

The series focuses heavily on Linux, especially Arch, because it is one of the most minimal and hence most universally adaptable distribution of Linux. Arch based distributions also come with some superpowers that other distros like debian don't provide. Let's take a deep dive into those exquisite abilities on this day.

### Arch Wiki

The ultimate manual for anything arch-related. The arch wiki and arch forums have everything you need regarding any issue you're facing or any mods you want to do to arch. Let's say you want to install gnome on your Arch that runs KDE-Plasma but don't exactly know how to do it. Just put in your issue with the suffix "arch wiki" in google.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705827310455/1096c746-40cc-4a1f-872a-b1222ce8d76a.png align="center")

The instructions rarely get outdated as the wiki is regularly updated with the latest information by the community (which is public and open). Some times the solutions proposed in arch wiki pages even work on non-arch based distributions if it is not a distro-specific problem.

### Arch User Repository (AUR)

Apart from The community maintained registry for arch linux packages. It is ginormous in terms of variety of packages. You can install almost any package from the AUR, be it Spotify, Discord or even Google-Chrome!

#### AUR helpers

Installing a package from the AUR, requires you to clone the repo and give the build command `makepkg -si` so that the system reads the MAKEPKG file.

MAKEPKG acts as a blueprint for building the package and adding it to system PATH.

However, AUR helpers assist in automating the build process. There are several apps like `yay` and `paru`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705828073036/37633216-0338-45cc-bfa7-b271b32be751.png align="center")

### Minimalism

Arch Linux provides us with the power to start from a minimal installation, which means that we decide what goes into our system, including even the kernel!

This helps avoid bloatware and enable for a lightning-fast system. Especially for developers when they combine their workflow with the clax.nvim neovim configuration.

### Self-development

Not only do we learn about partitioning, and different kinds of file systems, keymapping, audio servers and daemons, but also does installing arch help build a basic overview knowledge of foundations of an operating system.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1705828104991/d94fcd76-5f5b-4add-b28c-11bcdd642492.png align="center")

### Bleeding-edge updates

This is also a double-edged sword, bleeding-edge updates means that all of the system's packages are updated to the very latest version. If neovim's version on Debian is 0.6.1, it is 0.9.1 on Arch linux. But it also means that despite supporting newer technologies like lua configs in neovim, software and hence system may risk breaking due to the packages being too new and not being compatible with things like hardware.

Maintenance is also needed in Arch Linux, so we need to regularly make sure the system is updated. This is not an issue because it helps us stay more conscious of our system's workings.