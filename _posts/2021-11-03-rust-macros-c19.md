---
title: "Rust Macros"
date: 2021-11-03T10:37
categories:
  - Summary
  - Document
tags:
  - rust
  - c19
---


Contains a smorgasbord of advanced topics of interest, including unsafe Rust, macros, and more about lifetimes, traits, types, functions, and closures.

**Unsafe Rust**

opt out of some of Rust's guarantees and take responsibility for manually upholding those guarantees.


**Advanced traits**

associated types, default type parameters, fully qualified syntax, supertraits, and new type pattern in relation to traits.

**Advanced types**

new type pattern, type aliases, the never type, and dynamically sized types.


**Advanced functions and closures**

function pointers and returning closures.


**Macros**

The ways to define code that defines more code at compile time.


*What a macro is?*

The term `macro` refers to a family of features in Rust: declarative macros with `macro_rules!` and three kinds of procedural macros:

* custom `#[derive]` macros that specify code added with the `derive` attribute used on structs and enums
* attribute-like macros that define custom attributes usable on any item
* function-like macros that look like function calls but operate ont eh tokens specified as their argument


*Why we even need `macros` when we already have functions?*

macros are a way of writing code that writes other code, which is known as `metaprogramming`, for example, write Rust code that writes Rust code


*The additional power of macros*

* can take a variable number of parameters
* `macros` are expanded before the complier interprets the meaning of the code
  * `functions` get called at runtime and a trait needs to be implemented ar compile time

*downside*
* `macros` more complex than `functions` definitions


*How it works?*

Need to add more contents.
