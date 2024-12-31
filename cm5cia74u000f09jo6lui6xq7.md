---
title: "Memory Mirages"
datePublished: Tue Dec 31 2024 13:30:24 GMT+0000 (Coordinated Universal Time)
cuid: cm5cia74u000f09jo6lui6xq7
slug: memory-mirages
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735651721750/a7753d26-d8d5-4911-800d-79366dbb0404.png

---

Virtual memory is a method of using hardware and software to allow a computer to compensate for physical memory shortages, by temporarily transferring data from RAM to disk storage. It's a key component of modern computing, providing flexibility and efficiency in memory management.

## Concept of Paging and Virtual RAM

![Segmented, Paged and Virtual Memory](https://i.ytimg.com/vi/p9yZNLeOj4s/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLBhd1RhVr0cMqUBrwurpVFlyRE8Yg align="left")

Paging is a method of dividing a program's memory into blocks, or "pages". Each page is of a fixed size, typically 4KB. When a program runs, its pages are loaded into physical memory (RAM). If a program tries to access a page that isn't in memory, a "page fault" occurs. The operating system then loads the required page from disk into RAM.

Virtual memory extends the concept of paging, allowing programs to use more memory than physically exists on the computer. This is achieved by breaking down a process's memory requirements into smaller pieces (pages) and storing these pages non-contiguously in memory. Because each process is only using a fraction of their total address space, there is more memory left for other programs, improving CPU utilization and system throughput.

## Page Faults and Handling Them

A page fault occurs when a process accesses a memory page that isn't currently in physical memory. The memory management unit (MMU) raises an exception, and the operating system's kernel handles the exception by making the required page accessible in the physical memory or denying an illegal memory access.

When a page fault occurs, the operating system loads the required page from disk into RAM. This process is known as "demand paging". In an extreme case, no pages are swapped in for a process until they are requested by page faults. This is known as pure demand paging.

## Allocation of Frames

Frame allocation is an important task in virtual memory management. The absolute minimum number of frames that a process must be allocated depends on system architecture and corresponds to the worst-case scenario of the number of pages that could be touched by a single machine instruction. There are various allocation strategies, including equal allocation, proportional allocation, and allocation based on the priority of the process.

## Memory-Mapped Files

Memory-mapped files allow data files to be paged into memory the same as process files, resulting in faster accesses. A file is mapped to an address range within a process's virtual address space, and then paged in as needed using the ordinary demand paging system. File writes are made to the memory page frames, and are not immediately written out to disk. Some systems provide special system calls to memory map files and use direct disk access otherwise.

## Sources

* [Wikipedia - Page fault](https://en.wikipedia.org/wiki/Page_fault)
    
* [University of Illinois Chicago - Virtual Memory](https://www.cs.uic.edu/~jbell/CourseNotes/OperatingSystems/9_VirtualMemory.html)