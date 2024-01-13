---
title: "Coding in C"
datePublished: Tue Sep 05 2023 12:41:07 GMT+0000 (Coordinated Universal Time)
cuid: clm6aucw4000208mnesjl1bhf
slug: cic
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1693917643288/be07a26a-519a-4ed6-972f-6e416853419c.jpeg

---

Unlike Python, there's no real need to install C separately, It is already in our system. However, to execute C code, we need to setup a compiler. We will focus on using the GCC compiler here.

## Setup MinGW

To setup GCC on Windows, we must install [MinGW](https://sourceforge.net/projects/mingw/), which supports GCC on Windows.

We first install MinGW from SourceForge. And then run the executable.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693916637328/96fe1d4c-53f1-46cd-a333-aef7c1ead37b.webp align="center")

After we click 'Install' on the wizard, click next.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693916727605/299e58bb-0d96-49de-a51e-834d37a2ff3f.webp align="center")

Then we select whatever packages we need for C development:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693916775964/de9d3012-cba0-48fd-bc22-5b7b4da24274.png align="center")

Here, 'mingw32-base' and 'mingw32-gcc-g++' are best, so we only check those.

## Set Environment Variables

In order for MinGW to be accessible from any directory, and through any code editor like vscode by default, we must add it to our $PATH.

In order to do that, we search "environment variables" on the search bar, and open it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693917028671/4716d859-185d-4cd6-88b6-5ae7d4b6dac3.png align="center")

We click on environment variables at the bottom left.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693917064892/b6b759b8-ff1c-419b-89a7-e7bf8041f73e.webp align="center")

Then we click on 'PATH' and click on 'new', we paste the following and click OK

```bash
C:\MinGW\bin
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693917142641/fdcdc25d-70a0-4c35-81de-1e6081f033c9.jpeg align="center")

After we close all the windows, we can fire up our terminal and get started finally.

## Using GCC

In order to use GCC, we must first write a C file, it must have an extension of `.c`.

We first compile our code

```bash
gcc <file_name>.c -o <file_name>.exe
```

This will store the executable for our C code into another file with the same name (except the extension).

Then we run the file.

```bash
.\<file_name>.exe
```

We can also do all of this in one go.

```bash
gcc <file_name>.c -o <file_name>.exe && .\<file_name>.exe 
```

## Online alternatives

We can write and run our C code on online platforms like OnlineGDB or Replit as well.