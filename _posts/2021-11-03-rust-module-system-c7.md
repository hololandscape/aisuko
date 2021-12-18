---
title: "Rust Module System"
date: 2021-11-03T10:37
categories:
  - Summary
  - Document
tags:
  - rust
  - c7
---


Rust’s `module system` and about privacy rules for organizing your code and its public Application Programming Interface (API)

### The tools managing projects
* `Packages`: A Cargo feature that lets you build, test, and share crates
  * A package contains a `Cargo.toml` file that describes how to build those crates
* `Crates`: A tree of modules that produces a library of executable
* `Modules` and `use`: Let you control the organization, scope, and privacy of paths
* `Paths`: A way of naming an item, such as a struct, function


* `Crate` A crate is a binary or library
  * `crate root` is a source file that the Rust compiler starts from and makes up the root module of your crate
  * `src/main.rs` contains a binary crate
  * `src/lib.rs` contains a library crate

* `mod` keyword use to defined `mod`
  * can hold definitions for other items, such as structs, enums, constants, traits, functions 

### Paths for referring to an item in the Module Tree
* An *absolute path* starts from a crate root by using a crate name or literal `crate`
  * using the `crate` name to start from the crate root is like using `/` to start from the filesystem root in your shell
* A *relative path* starts from the current module and uses `self`, `super` or an identifier in the current module
  * Starting with a name means that the path is relative

* Bringing Paths into Scope with the use Keyword
  *  `use` keyword add a path into scope is similar to creating a symbolic link
  in the filesystem

* Re-exporting Names with `pub` `use`

Using External Packages(after Rust 2018 does not need this)

Using Nested paths to Clean Up large `use` Lists

__Code__
```
use std::io;
use std::io::Write;

// can be replace by the code below
use std::io::{self, Write};

// all both of them are add `io` and `Write` into the current scope
```

Create new `module`(mod)

```
mkdir src/sorting

// create mod functions
cat > src/sorting/bubble_sort.rs <<EOF
//bubble_sort
EOF

// create mod.rs load the bubble_sort into mod.rs
cat > src/sorting/mod.rs <<EOF
mod bubble_sort:

// load the bubble_sort at mod.rs
pub mod self::bubble_sort::bubble_sort;


//main.rs or lib.rs

pub mod sorting;

fn main(){
    use super::*;
    sorting::bubble_sort();
    assert();
}
```