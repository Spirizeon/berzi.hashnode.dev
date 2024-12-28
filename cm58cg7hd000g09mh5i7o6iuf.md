---
title: "What's a damn Syscall?"
datePublished: Sat Dec 28 2024 15:36:02 GMT+0000 (Coordinated Universal Time)
cuid: cm58cg7hd000g09mh5i7o6iuf
slug: whats-a-damn-syscall
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735397599998/666bf98f-54a4-46af-9828-5736079682cb.png

---

Welcome to this brand-new series, where we stray apart from the old conventional approach of randomly going through security stuff (like back in the ZySec series)

Today’s blog is more about CPUs, dealing with system calls (yeah syscalls), interrupts, etc.

## Origins: Binary → Hex → Asm → MLL → HLL

![Linux System Calls Under The Hood](https://juliensobczak.com/posts_resources/2021-08-10-linux-system-calls-under-the-hood/system-calls.png align="left")

Instead of coding architecture specific instructions, instructions were at one point written in Asm or Assembly language, and this could be the only human-understandable language that was closest to the processor.

Usually processors work in a **fetch-execute cycle** meaning a pointer goes through the input code and fetches the instructions one by one or line by line then executes them sequentially, then the pointer shifts to the next position or line and the entire cycle repeats. This pointer can be called the instruction pointer.

Slowly, as time went on, we wrapped asm specific instructions into libraries of mid-level languages (MLLs) like C and finally, to manage memory better, some techniques were further wrapped into libraries of high level languages like C++ and Python.

### That’s cool, But what’s a kernel?

![Linux0.11 kernel - kernel mode and user mode - Programmer Sought](https://blog.codinghorror.com/content/images/uploads/2008/01/6a0120a85dcdae970b0120a86db3ea970b-pi.png align="left")

When booting up the OS, the instruction pointer of the CPU must start somewhere. Enter the **kernel**. The kernel is the core of an operating system and has full/root/admin access to all of that system’s resources.

A processor hence has two modes usually, a user mode and a kernel mode. User modes often have restricted privileges like access to application specific code, permitted amounts of memory and I/O. Usually when these applications need to interact with drivers or need to do anything that requires system-wide access, we shift to kernel mode. How do we do that? Interrupts and system calls!

### Alright, Syscalls and Interrupts

![System Calls in Operating System Explained | phoenixNAP KB](https://phoenixnap.com/kb/wp-content/uploads/2023/08/system-call-steps-execution.png align="left")

It’s all about jumping between the kernel code and application codes which means shifting between kernel and user modes. To do this, we employ a mechanism known as interrupts. Interrupts help the CPU remember where the switch was made from user mode to kernel mode through saving the address of the pointer (or **handle**) of that memory location.

We use data structures known as Interrupt vector tables to do that (which is an entire topic in itself)

System calls are similar but very different to interrupts, being synchronous in nature unlike their asynchronous counterpart and moreover they focus more on the software aspect of things rather than bare-metal. These are used to request services from the operating system like asking to replicate a process, etc.

Few of the system calls are: open, read, fork and exit. Most system calls are made processor-specific. Wrappers to these system call functions are presented in libc in Unix-like systems and ntdll.dll in DOS based systems.