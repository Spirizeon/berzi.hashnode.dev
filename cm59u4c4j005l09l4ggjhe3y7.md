---
title: "Scheduling Quantums?"
datePublished: Sun Dec 29 2024 16:38:28 GMT+0000 (Coordinated Universal Time)
cuid: cm59u4c4j005l09l4ggjhe3y7
slug: scheduling-quantums
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735414354108/76b00fe0-2c3f-4b49-82c2-4f04d2050fbe.png

---

Let’s talk how processes are managed, to achieve that, let’s look at how switching works.

## Bursts

A CPU burst is the amount of time a process takes to complete, now this depends on whether the burst is purely CPU-bound or whether it has an additional condition on waiting for external input from the user (which would be an I/O burst)

## Timeslicing

The CPU basically pays attention to a particular processor for a specific time and then switches to another process, this is also an implementation to fake parallelism when we don’t have a multi-core processor. We call these interruptions as **preemptions** and the durations “timeslices”, or as the title says **Quantums**. The algorithms through which we create timeslices, organise and cycle them are known as **scheduling algorithms**. Linux uses something called a **Completely Fair Scheduler** and most modern operating systems employ a modified version of Round-Robin timeslice scheduling with process priorities and deadlines into account. A combination of all the timeslices for a process’s lifeline would be also a definition for a burst.

## Cooperation Vs. Preemption

Cooperative-based schedulers wait for the processes to complete entirely before we get started on fetching the next process. Unlike preemptive schedulers where the existing process is interrupted to switch to a new process. Preemptive scheduling employs a timer with an algorithm-dependent duration for process switching which helps deal with multiple processes as discussed before.

## Scheduling 101

We have a few examples for schedulers, let’s talk about them in detail:

### First Come First Serve (FCFS)

Also known as “First In, First Out” and popularly used to describe the Queues data structure. Priority is given to whatever processes are starting first and then the switch is made only when the current process is completed.

![Scheduling Algorithms (FCFS, SJF, SRTF, HRNN, RR, MLQ, MLQF) - Tutorial](https://static.takeuforward.org/content/-MH8adAmn align="left")

### Shortest Job First (SJN)

Shortest Job First, simply we deal with finding the process with the smallest CPU burst (now this entirely depends on how we predict the burst time though) and then we solve the processes accordingly.

![SJF Scheduling Illustration](https://static.takeuforward.org/content/-r0pleNsq align="left")

### Shortest Remaining Time First (SRTF)

It’s a modified implementation of SJN, where we have the instruction pointer checking for whether the remaining time for the current process is lesser than the the next process in queue.

![SRTF Scheduling Illustration](https://static.takeuforward.org/content/-5X9Ljlud align="left")

### Round Robin (RR)

Round Robins assigns fixed timeslices to each and every process, when the timeslice is over, processes are switched and cycled till they are over.

## Cool Stuff: HyperThreading

(coming on next issue)

## Scheduling 102

### Overheads and Starvation

Overhead is basically the extra amount of time spent by the CPU in switching contexts, system calls, etc. Starvation is when a process is left unfinished for a relatively long amount of time. We hence need to keep these two factors in mind along with the process type and priority when selecting a scheduling algorithm. Further we have some more strategies to solve these issues…

### Multiple-Level Queues (MLQ)

Despite the diagram suggesting 90% of the meaning of the term, each layer can have its own scheduling algorithm.

![Multilevel Queue Scheduling Illustration](https://static.takeuforward.org/content/-wsz3uWRR align="left")

### Extending MLQs with Feedback

To prevent starvation of processes, those that weren’t completed in time are shifted to a lower priority layer.

![Multilevel Queue with Feedback Scheduling Illustration](https://static.takeuforward.org/content/-r40OMD2_ align="left")