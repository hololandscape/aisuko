---
title: "Rust automated tests"
date: 2021-11-08T09:49
categories:
  - Summary
  - Document
tags:
  - rust
  - c11
---


All about testing, which even with Rust’s safety guarantees is necessary to ensure your program’s logic is correct


### The anatomy of a test function

A test in Rust is a function that's annotated with the `test` `attribute`
* `attribute` are metadata about pieces of Rust code
  * one example is the `derive` attribute
  * add `#[test]` on the line before `fn`

`cargo test` command will let Rust builds a test runner binary that runs the functions annotated with the `test` attribute and reports on whether each test function passes or fail


### Macros

* `assert_eq!` and `assert_ne!` macros use the operators `==` and `!=` respectively
* checking for panics with `#[should_panic]`, and the test will fail if the code inside the function doesn't panic

When the assertions fail, macros print their arguments using debug formatting, which means the values being compared must implement the `PartialEq` and `Debug` traits, and these traits usually as straightforward as adding the `#[derive(PartialEq, Debug)]` annotation to your struct or enum definition.


**Unit tests**

* `#[cfg(test)]` annotation on the tests module tell Rust to compile and run the test code only when you run `cargo test`, not when `cargo build`


**Integration tests**
*  `cargo test --test integration_test`

* `?` operator will return the error value from the current function for the caller to handle 

* `()` in the signature means we need to wrap the unit type value in the `Ok` value