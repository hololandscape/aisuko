---
title: "Rust common programming concepts"
date: 2021-11-02T19:47
categories:
  - Summary
  - Document
tags:
  - rust
  - c3
---


Covers Rust features similar to those of other programming languages.

* Constants 
  * using the const keyword instead of the let keyword type of the value must be annotated
  * constants can be declared in any scope, including the global scope

### Scalar Types
  * integers
    * like unsigned `u8` and signed `i8`
    * Signed and unsigned refer to whether it’s possible for the number to be negative
    * Signed numbers are stored using two’s complement representation
    * default integer type is `i32`, takes up 32 bits of space
      * this type is generally fastest, even on 64-bit systems
  * floating-point
    * `f32` `f64`
  * numbers
    * the basic mathematical operations
      * addition
      * subtraction
      * multiplication
      * division
      * remainder
  * booleans
  * characters
    * `char` literals are specified with single quotes
    * `char` type is four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII

### Compound Types
  * Compound types can group multiple values into one type
  * `tuple`
    * a general way of grouping together a number of values with a variety of types into one compound type
    * fixed length: once declared, they cannot grow or shrink in size
  * `array`
    * Arrays in Rust are different from arrays in some other languages because arrays in Rust have a fixed length, like tuples


### Functions

* We do declare their type after an arrow `->`
* the body of the function is a lonely `number` with no semicolon, because it's an expression whose value we want to return.

### Control flow
  * `loop`(err prone)
    * execute a block of code over and over again forever
  * `while`(err prone)
    * evaluate a condition within a loop
    * cons
      * can cause the problems to panic if the index value or test condition are incorrect
      * slow due to the compiler adds runtime code to perform the conditional check of whether the indec
      is within the bounds of the array on every iteration through the loop
  * `for`
    * `..` is a range operator,which forms a Range<Idx> object(or a derivative `RangeFrom`,`RangeFull` or `RangeTo`)
      those objects only contain indexes(the Idx type), so you can rest assured that `.len()` is only evaluated once.