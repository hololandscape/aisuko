---
title: "Rust Traits And Lifetimes"
date: 2021-11-03T10:56
categories:
  - Summary
  - Document
tags:
  - rust
  - c10
---



Digs into generics, traits, and lifetimes, which give you the power to define code that applies to multiple types



### Contents
* Generic Data types
* Traits
* Validating References with Lifetimes


### Generic Data Types

Generic eliminate the duplication by introducing a generic parameter in a single function


```
// This definition as: the function `largest` is generic over some type `T`
fn largest<T>(list: &[T]) -> T {}
```

#### Generic data types and it performance in Rust

* support function
* support structure
* support enum
* support method

```
// By declaring T as a generic type after impl, 
// Rust can identify that the type in the angle brackets in Point is a generic type rather than a concrete type.
impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}
```

* performance of code using generics
  * Rust implements generics(accomplishes by performing `Monomorphization` of the code at compile time) doesn't run any slower using generic types than it would with concrete type

  * `Monomorphization` is the process of turing generic code into specific code(replacing the generic definition with the specific ones)
    by filling in the concrete types that are used when complied

  * Rust compiles generic code into code that specifies the type in each instance(`monomorphization`), we pay no runtime cost for using generics


### Traits defining shared behavior

Traits are similar to a feature often called `interface`, but although with some differences.

  * a `trait` tells the Rust compiler about functionality a particular type has and
  can share with other types, so we can use traits to define shared behavior in an abstract way

  * we can use traits to define shared behavior in an abstract way
  
  * implementing a trait on different type
  
  * `trait` can be implement by default
    * the `trait` can be called the function was defined under the `trait`
  
  * `trait` as parameters
    * use trait to define functions that accept many different types
    * returning types that implement traits
    * specifying multiple trait bounds with the `+` Syntax
    * Clearer Trait Bounds with `where` Clauses

    ```
    // Summary is a struct
    // any type that implements the specified trait can be accept as parameter
    // syntax sugar for trait bound
    // and support 
    pub fn notify(item: &impl Summary){
        println!("Breaking news! {}", item.summarize());
    }
    ```
 
  * `trait` 
    * trait as parameters for a longer form(with generic type) is called `trait bound`

    ```
    // can express more complexity in other cases
    pub fn notify<T: Summary>(item: &T) {
        println!("Breaking news! {}", item.summarize());
    }

    ```  

  * `+` syntax
    * specify more than one `trait` bound
  
  * clearer trait bounds with where `clauses`
    * too many trait bounds has its downside, lots of trait bound information between the function's
    name and its parameter list, making the function signature hard to read
    * so the alternative syntax for specifying trait bounds inside a where clause after the function
    signature.

    ```
    // from
    fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {
    // to 
    fn some_function<T, U>(t: &T, u: &U) -> i32
        where T: Display + Clone,
              U: Clone + Debug
    {
    ```

### Validating references with Lifetimes

This feature let Rust has enough information to allow memory-safe operations and disallow operations that would create dangling pointers or otherwise violate memory safety.

* this lifetime means to `reference and borrowing`
* Rust determine the code invalid uses a borrow checker
  * the Rust has a borrow checker that compares scopes to determine whether all borrows are valid

* lifetime annotation syntax
   * syntax 
     * `the names of lifetime parameters must start with an apostrophe(') and are usually all lowercase and very short, like general types and most people use the name 'a`
     * usually all lowercase and very short, like general types
     * place lifetime parameter annotations after the `&` of a reference, using a space to separate the annotation from the reference's type
    
* lifetime annotation in function signatures
  * We’ve told Rust that the lifetime of the reference returned by the `longest` function is the same as the smaller of the lifetimes of the references passed in
  
* thinking in terms of lifetimes
  * the way in which you need to specify lifetime parameters depends on what your your function is doing
  
* lifetime annotations in struct definitions
  
* lifetime elision
  * lifetime on function or method parameters are called `input lifetimes`
  * on return values are called `output lifetimes`
  * `three rules` figure out what lifetimes references have when there aren't explicit annotations
    * first rule applies to input lifetimes
      * each parameter that is a reference gets its own lifetime parameter
    * second and third rules apply to output lifetimes
      * one input lifetime parameter lifetime is assigned to all output lifetime parameters
    * third rule is multiple input lifetime parameters, but one of them is `&self` or `&mut self`(because this ia a method), the lifetime of `self` is assigned to all output lifetime parameters 
  
* lifetime annotations in method definitions
  * declared after the `impl` keyword and then used after the struct's name, because those lifetimes are part of the struct's type
  
* the static lifetime
  * all string literals have the `'static` lifetime, which we can annotate as follows
  * which means that this reference can live for the entire duration of the program
  
* generic type parameters, trait bounds and lifetimes together

