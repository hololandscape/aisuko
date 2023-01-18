---
title: "GNU Linux Process"
categories:
  - Document
tags:
  - GNU/linux
  - process
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


In computing, a process is the instance of a computer program that being executed by one or many threads. It contains the program code and its activity. 


![processing](https://upload.wikimedia.org/wikipedia/commons/thumb/2/25/Concepts-_Program_vs._Process_vs._Thread.jpg/1280px-Concepts-_Program_vs._Process_vs._Thread.jpg){: .align-center}


## Representation

The computer system process consists of the following resources:

* An `image` of the executable machine code associated with a program

* Memory(typically some region of `virtual memory`)
  * Includes the executable code
  * Process-specific data(input and output)
  * a `call stack` to keep track of active subroutines and/or other events
  * a `heap` to hold intermediate computation data generated during run time
* Operating system descriptors of resources that are allocated to the process, such as `file descriptors`(Unix terminology) or `handles`(Windows), and data sources and sinks.
* `Security` attributes, such as the process owner and the process' set of permissions(allowable operators)
* `Processor` state(`context`), such as the content of registers and physical memory addressing. The state is typically stored in computer registers when the process is executing, and in memory otherwise.


### What's the `call stack`?

In computer science, a call stack is a stack data structure that stores information about the active subroutines of a computer program.


The operating system holds most of this information about active processes in data structures called process control blocks. Any subset of the resources, typically at least the processor state, may be associated with each of the process' threads in operating systems that support threads or child processes.


The operating system keeps its processes separate and allocates the resources they need, so that they are less likely to interfere with each other and cause system failures.


### Multitasking an process management

A multitasking operating system may just switch between processes to give the appearance of many processes executing simultaneously(parallel), though in fact only one process can be executing at any one time on a single CPU (unless the CPU has multiple cores, then multithreading or other similar technologies can be used).


### Inter-process communication

When processes need to communicate with each other they must share parts of their address spaces or use other forms of inter-process communication(IPC). For instance in a shell pipeline, the output of the first process need to pass to the second one, and so on; another example is a task that can be decomposed into cooperating but partially independent processes which can run at once.


## Reference

[Process(computing)](https://en.wikipedia.org/wiki/Process_(computing))