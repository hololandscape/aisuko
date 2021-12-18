---
title: "Linker(computing)"
date: 2021-11-01T08:54
categories:
  - Blog
tags:
  - rust
  - compiler
  - linker(computing)
---

The Linker use in Rust cross platform like:

```
# list the all the target
rustc --print target-list
```

Add the target and the complier to your host environment before you run `cargo build`

```
$ mkdir .cargo
$ cat >.cargo/config <<EOF
> [target.x86_64-unknown-linux-gnu]
> linker = "x86_64-linux-gnu-gcc"
> EOF

```

And if you work on Mac for Linux, you need to install `x86_64-linux-gnu-gcc` use `brew install FiloSottile/musl-cross/musl-cross` or `brew install gcc`.

Use [`rustup`](https://rust-lang.github.io/rustup/cross-compilation.html) to add the target

```
$ rustup target add arm-linux-androideabi
info: downloading component 'rust-std' for 'arm-linux-androideabi'
info: installing component 'rust-std' for 'arm-linux-androideabi'
```


### Contents

* Linker(computing)

**What's the Linker?**

In computing, , a linker or link editor is a computer system program that takes one or more object files and combine them into a single executable file, library file, or another "object" file.


The simper version of linker

A simpler version that writes its output directly to memory is called the loader, though loading is typically considered a separate process.


**Concepts**

Computer programs typically are composed oof several parts or modules; these parts/modules do not be contained within a single object file, and in such cases refer to each other by means of symbols as addresses into other modules, which are mapped into memory addresses when linked for execution.(Such as C# and Golang)

Typically, an object file can contain three kinds of symbols:

* defined "external" symbols, sometimes called "public" or "entry" symbols, which allow it to be called by other modules
* undefined "external" symbols, which reference other modules where these symbols are defined
* local symbols, used internally within the object file to facilitate relocation

For most compilers, each object file is rhe result of compiling one input source code file. When a program comprises multiple object files, the linker combines these files into a unified executable program, resolving the symbols as it goes along.

Linkers can take objects from a collection called a library or runtime library. Most linkers do not include the whole library in the output; they include only the files that are referenced by other object files or libraries. Library linking may thus be an iterative process, with some referenced modules requiring additional modules to be linked, and so on.


The linker also takes care of arranging the objects in a program's address space.

  * Since a compiler seldom knows where an object will reside, it often assumes a fixed `base location`
  * Relocating machine code may involve re-targeting of absolute jumps, loads and stores


**How to keep there is no conflict the programs load at the same base address?**

The executable output by the linker may need another relocation pass when it is finally loaded into memory(just before execution). This pass is usualy omitted on hardware offering virtual memory: every program is put into its own address space.



**Dynamic linking/linker**

Not all the operating system environments allow dynamic linking, deferring the resolution of some undefined symbols until a program is run. This means that the executable code still contains undefined symbols, plus a list of objects or libraries that will provide definitions for these.

Advantages:

* Often-used libraries: need to be stored in only one location
* If a bug in library function is corrected by replacing the library, all programs using it dynamically will benefit from the correction after restarting them.


Disadvantages:

* like `.dll`(Windows), an incompatible updated library will break executables that depended on the behavior of the previous version of the library if the newer version is incorrectly not backward compatible.( like .net framework project lose a `.dll`)

* a program, together with the libraries it uses, might be certified as a package, but not if components can be replaced.


**Static linking**

* The result of the linker copying all library routines used in the program into the executable image.This require more disk space and memory than dynamic linking, but is more portable, since it does not require the presence of the library on the system where it runs.


**Relocation**

* As the compiler has no information on the layout of objects in the final output, it cannot take advantage of shorter or more efficient instructions that place a requirement on the address of another object

* Automatic jump-sizing(jump optimizations), this step can be performed only after all input object have been read and assigned temporary addresses(Need more detail like What's the offset from the current location)

* While instruction relaxation typically occurs at link-time, inner-module relaxation can already take place as part of the optimizing process at compile-time.In some cases, relaxation can also occur at load-time as part of the relocation process or combined with dynamic dead-code elimination techniques.





**Knowledge**

Object files: a computer file contain object code, that is the machine code and out of compiler or assembler.

Relocation: the process of assigning load addresses for position-dependent code and data of a program and adjusting the code and data to reflect the assigned address.


### Reference Links

https://stackoverflow.com/questions/41761485/how-to-cross-compile-from-mac-to-linux  
https://en.wikipedia.org/wiki/Linker_(computing) 
https://en.wikipedia.org/wiki/Relocation_(computing)  
https://en.wikipedia.org/wiki/Object_file  





