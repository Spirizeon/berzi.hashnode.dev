---
title: "Zysec Recharged: Month #2"
datePublished: Mon Apr 22 2024 12:31:01 GMT+0000 (Coordinated Universal Time)
cuid: clvaxrawg000509l9gy6d58zf
slug: zysec-recharged-month-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1712671527377/edd6789d-1ab8-4aad-897a-db05808fa800.png

---

## Specifications and setup:

You need a pretty solid rig for development and testing across different platforms. Also, you will need heavyweight development tools (which will be mentioned later on). Anyways, here are some recommended specifications for a system for malware development:

* Least 16GBs of DDR4/5 RAM
    
* Least 6 core CPU with 10+ threads
    
* 1TB/512GB SSD/HDD (SSD preferred tho)
    
* Good cooling system
    

Ideally, a gaming laptop or rig would help you achieve this, or you can simply use cloud VMs on Linode to prepare a lab.

Here are the tools that you may require for the lab:

* Visual Studio 20xx (community/professional)
    
* Oracle Virtualbox/VMware workstation player
    
* Kali Linux
    
* Windows 10/11
    
* Process Hacker
    
* x64dbg
    

## Fundamentals

Firstly you should be knowing that **malware is usually made for windows-based** systems. So we will be focusing on developing malware that is meant to **work with windows**. For that we need to know how to manipulate things like threads and processes in windows. A great place to start would be the **Win32** API. This helps you program windows to do certain tasks, from both high and low level perspectives.

Also, make sure you are familiar with:

* windows-fundamentals (also would REALLY help if you've ever used windows in your life before).
    
* C language and bit of assembly
    
* metasploit-framework
    
* virtualization (coz we ain't detonating malware on our own computer)
    

## The Dive: How to jump in

The best way to learn something is by trying it out first then going deeper theory wise. That being said, let's build malware... (Oh and btw,don't forget to turn off all AVs while building or running it)

## Process Injection (Shellcode based)

Shellcode is compiled code written in machine language, that in malware language attempts to make itself run on the system by activities like injecting it into a process.

We can write our own shellcode by compiling our C code. Or we can let tools like `msfvenom` do the job.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1713788226213/7f08d6c5-4f82-4742-b90d-f9ccd0cbebe4.png align="center")

Here's how process injection works in layman terms. We grab a process that's already running, then proceed to capture its process ID (which makes it unique). Now, under the same process ID, we allocate part of the memory. Then we inject shellcode into it. Then, we run it through starting a thread (consider a thread like a candle wick which lights up when started)

So, while the original process is running, our shellcode runs along with it in the background.

if you want to check out an example on shellcode injection, see my repo [RootBlast](https://github.com/spirizeon/rootblast)

## Problems with writing malware

* It's difficult to find resources, mostly it'll be blogs and articles because mainstream platforms ban such content
    
* You need to study a LOT about OS related stuff, especially windows
    
* You may get arrested (Ok, that's a joke, unless you're not careful)
    
* AV/EDRs are constantly evolving so reading about how to make your malware undetectable is a must
    

## On the next issue

I'll talk about some more types of malware and also AV/EDR evasion techniques. Thank you for reading.

## Resources

* [https://www.crow.rip/crows-nest/mal/dev/getting-started](https://www.crow.rip/crows-nest/mal/dev/getting-started)
    
* [https://github.com/r3p3r/nixawk-awesome-windows-exploitation](https://github.com/r3p3r/nixawk-awesome-windows-exploitation)
    
* [https://scholar.google.com/](https://scholar.google.com/)