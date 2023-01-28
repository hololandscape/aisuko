---
title       : "Introduction to EECS"
excerpt     : "Introduction to EECS"
sitemap     : false
permalink   : /docs/mit_6_01SC/
toc         : true
---

Deciding how to make trade-off is a crucial part of engineering. Programs should never be a mystery to you.


## Overview
Modularity, abstraction and modeling
* Modularity is the idea of building components that can be re-used
* Abstraction is the idea that after constructing a module(be it software or circuits or gears)

<iframe src="https://hostux.social/@aisuko/109765016605390102/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>


* The concept about `compilers` or `interpreters`
The languages are converted into instructions in the computer's native machine language by other computer programs

* The one about the choice of programming language
The choice of programming language is primarily a matter of taste and convenience

### Models
It is a new system that is considerably simpler than system being modeled, but which captures the important aspects of the original system.

* Analytical models
* Synthetic models
* Internal models
* Data structures


## Programs and Data
The object-oriented programming will give us methods fpr capturing common patterns in data and the procedures that operate on that data, via classes, generic functions, and inheritance.

The meaning of computer programs by understanding how the interpreter operates on them.

Interpreter
  * Programs are understood and executed by a computer program called an interpreter
  * The `reader` or `tokenizer` takes as input a string of characters and divides them into `tokens`, which are numbers, words(like while or a) and special characters(like :)
  * The `parser` takes as input the string of tokens and understands them as constructs in the programming language, such as while loops, procedure definitions, or return statements
  * The `evaluator`(which is also sometimes called the interpreter, as well) has the really interesting job of determining the value and effects of the program that you ask it to interpret
  * The `printer` takes the value returned by the evaluator and prints it out fo the user to see

### 3.1 Primitives
Primitive data(integers, floating point numbers, and strings)
  * Data structures(lists, arrays, dictionaries and records)
Abstract data types
  * It provides a way of abstracting away from representational details and allowing us to focus on what the data really means.

### 3.3 Structured data
List mutation and shared structure
A tuple is a structure that is like a list, but it not mutable. `String` is a special kind of tuple.

* Lambda constructor
  `lambda <var1>, ..., <varn> : <expr>`

* Recursive
  * The base case
  * Recursive case
