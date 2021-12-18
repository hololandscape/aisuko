---
title: "Rust Struct Method Associate Functions"
date: 2021-11-08T11:13
categories:
  - Summary
  - Document
tags:
  - rust
  - c5
---



Discusses the struct, method and associate function


### Contents
* Struct
* Adding Useful Functionality with Derived Traits
* Method Syntax
* Summary


### Struct

The entire instance of `Struct` must be mutable, Rust doesn't allow us to mark only certain fields as mutable.


##### Similar to tuples
* the pieces of s struct can be different types
* (more flexible than tuples) don't have to rely on he order of the data to specify or access the values of an instance.
* Using the Field Init Shorthand when Variables and Fields Have the Same Name(`same effect with less time`)


###### Struct Update Syntax
Creating instances from other instances with `struct update syntax`
* the syntax `..` specifies(`same effect with less time`) that the remaining fields not explicitly set should have the same value as the fields in the given instance, e.g `..user1`


```
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    let user2 = User {
        email: String::from("another@example.com"),
        // struct update syntax
        ..user1
    };
}

```

Tuple struct just have the types of the fields.

```
fn main() {
    struct Color(i32, i32, i32);
    struct Point(i32, i32, i32);

    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

Each struct you define is its own type, even though the fields within the struct have the same types.  

We want to borrow the struct rather than take ownership of it, use the `&`(reference) in the function signature


### Adding Useful Functionality with Derived Traits

* [Traits]the `derive` annotation can add useful behavior to our custom types
* using `dbg!` macro, calling the dbg! macro prints to the standard error console stream (stderr), as opposed to `println!` which prints to the standard output console stream (stdout).


### Method Syntax

Methods are different from functions in that they're defined within the context of a struct(or an enum or a trait object), and their first parameter is always `self`, which represents the instance of the struct the method is being called on.


**Defining Methods**

* `impl` (implementation) block, and the first parameter is `&self` that means the method can be invoke by the struct instance
* `&self` is actually short for `self: &Self`, within an `impl` block, the type `Self` is an alias for the type that the `impl` block is for

* `->`(arrow) operator in `C` and `C++`
  * use `.` to call a method on the object directly
  * use `->` call the method on a pointer to the object
  * if `object` is a pointer, `object->something()` is similar to `(*object).something()`
  * Rust doesn’t have an equivalent to the `->` operator; instead, Rust has a feature called automatic referencing and dereferencing

* when you call a method with `object.something()`, Rust automatically adds in `&`, `&mut`, or `*` so object matches the signature of the method

* Given the receiver and name of a method, Rust can figure out definitively whether the method is:
  * `reading (&self)`
  * `mutating (&mut self)`
  * `consuming (self)`


**Associated Functions**

All functions defined within an `impl` block are called associated functions because they’re associated with the type named after the `impl`. We can define associated functions that don't have `self` as their first parameter(and thus are not methods) because they don't need an instance of the type of work with.  

To call `associated functions`, we use the `::` syntax with the struct name.


### Summary

* `struct` let you create custom types that meaningful for you domain
* `method` specify the behavior that instances of your struct have
* `associated functions` let you namespace functionality that is particular to your struct without having an instance available 