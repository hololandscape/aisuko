---
title: "Cross compiler"
date: 2021-10-31T16:47:00
categories:
  - Blog
tags:
  - rust
  - cross compiler
  - compiler
---


I'd like to try to create a tool help to install docker on any debian series operating system with Rust language. So, we need to face to the cross platform build of Rust. 


#### What's the mean of `no runtime` in Rust?

Reference: [Rust official chapter 16](https://doc.rust-lang.org/book/ch16-01-threads.html#using-threads-to-run-code-simultaneously)


Runtime is a confusing term and can have different meanings in different contexts.

And we know that assembly language does not have runtime code. So, we can get the result that non-assembly language always have some amount of runtime code, and the code can be large
or small depending on the language. 

And the runtime we mean code that is included by the language in every binary.


* Pros
  * smaller binaries can easier to combine the language with other languages in more context

* Cons
  * fewer features(for example, the green-threading M:N model requires a larger language runtime to manage threads)

In conclusion, colloquially when people say a language has "no runtime" they often mean "small runtime". And in order to does not compromise on performance, Rust needs to have nearly no runtime and can call into C. And we already to know the means of `no runtime` and it is not relate to the cross platform. 



### Contents

* Cross compiler



### Cross compiler



A **cross compiler** is a compiler capable of creating executable code for a platform other than the one on which the compiler is running. For example, a compiler that runs on a PC but generates code that runs on Android smartphone is a cross compiler.

A cross compiler is for cross-platform software generation of machine code, and separate the build environment from target environment.

And there several situations:

* Embedded computers
* Compiling for multiple machines
* Compiling on a server farm
* Bootstrapping to a new platform
* Compiling native code for emulators for older no-obsolete platforms
  * likes the Apple 2

* Use of virtual machine(JVM) can resolves some of the reasons for which cross compilers were developed. But virtual machine are often slower and the compiled program can only be run on computers with that virtual machine.




**Canadian Cross**

Canadian Cross with GCC the number of compilers involved
  * the proprietary native compiler for machine A (1) is used to build the gcc native compiler A(2)
  * the gcc native compiler for machine A(2) is used to build the gcc across compiler from machine A to machine B(3)
  * tge gcc cross compiler from machine A to machine B(3) is used to build the gcc cross compiler from machine B too machine C(4)


![](https://upload.wikimedia.org/wikipedia/commons/c/cb/Example_of_Canadian_Cross%2C_scheme.svg)


**The flow of below**
  
proprietary native compiler -> gcc native compiler -> gcc across compiler -> gcc cross compiler




**GCC and cross compilation**

`GCC`(GNU Compiler Collection), a free software collection of compilers, can be set up to cross compile. It supports many platforms and languages.

GCC requires that a compiled copy of `binutils` be available for each targeted platform. Especially important is the GNU Assembler.

Therefore, binutils first has to be compiled correctly with thw switch `--target=some=target` send to the configure script. GCC also has to be configured with the same `--target` option.

GCC can then be run normally provided that the tools, the `binutils` creates, are available in the path.

GCC requires that a portion of the target platform's C standard library(libc) be available on the host platform. But the alternative can use `newlib`(smaller C library containing only the most essential components required to compile C source code).

GNU autotools packages(autoconf, automake, and libtool) use the notion of a build platform, a host platform, and a target platform.




**Knowledge**

* **Clang** is natively a cross compiler, at build time you can select which architectures you want Clang to be able to target.

* Libraries like **Qt** and its predecessors including XVT provide source code level cross development capability with other platforms

* GCC(GNU Compiler Collection): a optimizing compiler produced by the GNU project, supporting various language and hardware architectures and operating systems.

* GNU Assembler: the default backend of GCC and part of the GNU Binutils package. It's used to assemble the GNU operating system and the Linux Kernel, and various other software.

* binutils(GNU Binaries Utils): a set of programming tool for creating and managing the binary programs, object files, libraries and profile data and assembly source code.

* configure script: is an execute script designed to aid in developing a program to be run ona wide number of different computers.



### Reference links:

https://en.wikipedia.org/wiki/Linker_(computing)  
https://en.wikipedia.org/wiki/Cross_compiler  
https://github.com/japaric/rust-cross#cross-compiling-with-cargo  
https://stackoverflow.com/questions/41761485/how-to-cross-compile-from-mac-to-linux  
https://doc.rust-lang.org/nightly/rustc/platform-support.html#tier-1-with-host-tools  
