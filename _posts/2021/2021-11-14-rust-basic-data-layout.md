---
title: "Basic data layout"
date: 2021-11-14T15:02
categories:
  - Summary
  - Document
tags:
  - rust
  - linked-list
  - data-layout
---


For my personal opinion, we need to use the knowledge to make effect to industry. People still limit by the energy and time.  

[I follow this idea](https://hololandscape.github.io/blog/blog/never-needed-yet/)


### What's the `tag` of the enum in Rust?

The tag help us to create less junk.


### What's the junk of data layout?

This need to look at how an enums is laid out in memory.

* allocating the empty in memory

### Null pointer optimization

Make the whole object be 0 if the pointer is null, help avoid waste more even space.  

Rust enum layout totally unspecified to support this kind of optimization.  

null pointer lets `&`, `&mut`, `Box`, `Rc`, `Arc`, `Vec` and several other important types in Rust have no overhead when put in an Option(this should be more explain).  

### How to avoid extra junk?

* use the list never allocates extra junk(the data-structure should use the type which implements null pointer optimization)
* the elements are uniformly allocated





__Source Of Read__

* [rust unofficial](https://rust-unofficial.github.io/too-many-lists/first-layout.html)