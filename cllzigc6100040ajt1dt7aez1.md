---
title: "Supercharge productivity through local development on Android"
datePublished: Thu Aug 31 2023 18:39:46 GMT+0000 (Coordinated Universal Time)
cuid: cllzigc6100040ajt1dt7aez1
slug: cldba
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693507179605/26be4e05-d1ad-41b3-a3f0-64b18edf1b8a.png

---

### What's Termux?

Termux is **a free and open-source terminal emulator for Android** that allows for running a Linux environment on an Android device. (NOTE: Android is a separate OS, although it has a modified version of the Linux kernel, which is open source)

### Installing Termux

Termux can be installed either through the **Play-Store** or **F-Droid**.

### Setup

Presently, at the time of this blog being written, Termux's official repo seems to have issues that prevents installation of packages.

#### Changing to another repo mirror

we simply switch the repository from which we are supposed to install our pakcages. For that, we type in:

```bash
$ termux-change-repo
```

We then select the main-repo

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693506292372/5bc08231-bd0c-4ae3-bbd1-72f6695d61d3.png align="center")

Then, we switch our repo to the A1batross mirror (recommended)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693506316801/f59be0c9-b578-4720-bc6f-0c149b163b32.png align="center")

After pressing 'OK', we return to the terminal.

Now, We install and extract some essential packages

```bash
$ apt upgrade
```

At certain points, the user may be prompted to press some keys like Y/N, or simply choose Y or the default ones.

### Programming

Time to Code, let's take compiled languages like C for example. We need GCC/Clang for that. Fortunately, Clang can be installed on Termux through the following command:

```bash
$ apt install clang -y
```

We will now need an editor to write our C code, let's install a command-line-based editor since we don't have a GUI on Termux by default. We can choose either Nano or Vim

```bash

$ apt install vim #or you can "apt install nano"
```

Now that our code editor and compiler are ready, we can start programming and then run the program by:

```bash

$ clang <file-name>.c -o <file-name> 
$ ./<file-name>
```

The first command converts the C code into a binary file and saves it in another file with the same name

The second command runs the binary file to give the output (if any).

This is the end of the article. If you liked it, please check out how to emulate a full-fledged Linux distribution on Termux [here](https://zyree.hashnode.dev/portable-linux).