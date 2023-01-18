---
title: "Rust cargo commands and features"
date: 2021-11-08T15:56
categories:
  - Summary
  - Document
tags:
  - rust
  - c1
  - c2
---



#### Initial the project

The information of how to setup and initial the project and how to use `cargo` command.

#### Contents

* Install
* Language features
* Cargo


**Install**

* Install the latest stable version of Rust using `rustup`
* Write and run a “Hello, world!” program using `rustc` directly

* Using a ! means that you’re calling a macro instead of a normal function

**Language Feature**
* Rust is an ahead-of-time compiled language
* Rust is a strong type check language
* Rust allows us to shadow the previous value with a new one
  * This feature is often used in situations in which you want to convert a value from one type to another type
* `u32` seen here is an unsigned `32-bit` integer

```
let guess: u32 = guess.trim().parse().expect("Need a number");
```

**Cargo**

* Cargo is Rust’s build system and package manager
  * building your code
  * downloading the libraries your code depends on
  * `cargo check` just check the code can be complies does not produce an executable
  * `cargo build` only build and produce an executable `./target/debug`
  * `cargo run` build and run
  * `cargo build --release` build and optimizations for benchmark and production `target/release`
  * `cargo test -- sub-mod name`
