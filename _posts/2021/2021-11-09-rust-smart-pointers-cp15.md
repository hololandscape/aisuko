---
title: "Rust Smart Pointers"
date: 2021-11-09T19:24
categories:
  - Summary
  - Document
tags:
  - rust
  - c15
---



Discusses smart pointers that the standard library provides and the traits that enable their functionality.  

A pointer is a general concept for a variable that contains an address in memory. References are indicated bt the `&` symbol and borrow the value they point to,the pointer enables you to have multiple owners of data by keeping track of the number of owners and, when no owners remain, cleaning up the data.

Smart pointers are data structures not only act like a pointer but also have additional `metadata` and `capabilities`. e.g `Vec<T>` own some memory and allow you to manipulate it, and also have metadata(such as their capacity) and extra capabilities or guarantees(such as with `String` ensuring its data will always be valid UTF-8).  

Smart pointers are usually implemented using structs. And implement the `Deref` and `Drop` traits. The `Deref` trait allows an instance of the smart pointer struct to behave like a reference so you can write code that works with either references or smart pointers. The `Drop` trait allows you to customize the code that is run when an instance of the smart pointer goes out of scope.


### Contents
* `Box<T>` for allocating values on the heap
  * `Deref`
  * `Drop`
* `Rc<T>` a reference counting type that enables multiple ownership
* `Ref<T>` and `RefMut<T>`
* `RefCell<T>`, a type that enforces the borrowing rules at runtime instead of compile time
* References cycles


### Box<T>

##### Using Box<T> to point to data on the heap

Boxes don't have performance overhead, but they don't have many extra capabilities either, and use them most in these situations:

* a type whose size can't be known at compile time and you want to use a value of that type in a context that requires an exact size
* a large amount of data and you want to transfer ownership but ensure the data won't be copied when you do so
  * to improve performance in this situation, we can store the large amount of data on the heap in a box. then, only the small amount of pointer data is copied around on the stack
* want to own a value and you care only that it;s a type that implements a particular trait rather than being of a specific type known as a *trait object*

##### Enabling recursive types with boxes

At compile time, Rust needs to know the space a type takes up. one type whose size can't be known at compile time is a `recursive type`, where a value can have as part of itself another value of the same type. The `recursive type` nesting of values could theoretically continue infinitely, so Rust doesn't know much space a value of a recursive type needs boxes have a known size.  

###### `cons list`

`cons list` is a data type common in functional programming languages comes from the lisp programming language and its dialects.

In Lisp, the `cons` function constructs a bew pair from its two arguments, usually are a single value and another pair, these pairs containing paris form a list. Each item in a cons list contains two elements: the value of current item and the next item. The last item in the list contains only a value called `Nil` without a next item. Most of time when you have a list of items in Rust, `Vec<T>` is a better choice to use.

##### Using Box<T> to get a recursive type with a known size

A `Box<T>` is a pointer, the pointer's size doesn't change based on th amount of data it's pointing to. And `Boxes` provides only the indirection and heap allocation, they don't have any other special capabilities. And the `Box<T>` type is smart pointer because it implements the `Deref` trait, which allows `Box<T>` values to be treated like references. When a `Box<T>` value goes out of scope, the heap data that the box is pointing to is cleaned up as well because of the `Drop` trait implementation.


#### Deref Trait

Implementing the `Deref` trait allows you to customize the behavior of the `deference operator *` implement `Deref` in such a way that a smart pointer can be treated like a regular reference.  

Defining our own smart pointer to enable dereferencing with the `*` operator, the type need to implement the `Deref` trait. `deref` method returns a reference to value, and the plain dereference outside the parentheses in `*(y.deref())` is still necessary due to the ownership system. 

##### Implicit `deref coercion` with functions and methods

Deref coercion happens automatically when we pass a reference toa particular type's value as an argument to a function or method that doesn't match the parameter type in the function or method definition.(e.g: convert `&String` to `&str` )

```
use std::ops::Deref;

impl<T> Deref for MyBox<T>{
  // `type Target =T` defines an associated type for the `Deref` trait to use.(cp19)
  type Target =T;

  fn deref(&self) -> &Self::Target{
      // deref returns a reference to the value we want to access with the `*` operator
      &self.0
  }
}
```

* runtime penalty

Rust is pre-compile, so will analyze the types and use `Deref::deref` as many times as necessary to get a reference to match the parameter's type. The number of 
times that `Deref::deref` needs to be inserted is resolved at compile time.

##### Deref Coercion Interacts with Mutability

Use the `DerefMut` trait to override the `*` operator on mutable references.  

* From `&T` to `&U` when `T: Deref<Target=U>`
* From `&mut T` to `&mut U` when `T: DerefMut<Target=U>`
* From `&mut T` to `&U` when `T: Deref<Target=U>`
  * coerce a mutable reference to an immutable one, but the reverse is not possible due to the borrow rules(borrow rules doesn't guarantee that)

#### Running code on cleanup with the Drop trait

This smart pointer pattern lets you customize what happens when a value is about to go out of scope, and can implementation for `Drop` on any type.  

In Rust, the free memory code will insert whenever the value goes out of scope automatically by the compiler. And the code by implementing the `Drop` trait.

* Variable are dropped in the reverse order of their creation.


##### Dropping a value Early with `std::mem::drop`

Using smart pointers that manage locks and want to force the `drop` method that release the lock. Rust doesn't allow call the `Drop` trait's `drop` method manually(this can double free error); instead you have to call the `std::mem::drop` function provided by the standard library.


### Rc<T>, the `Reference Counted Smart Pointer`


To support multiple ownership, use type called `Rc<T>`, which is an abbreviation for reference counting. The `Rc<T>` type keeps track of the number of references to a value to determine whether or not the value is still in use. Zero references to a value, the value can be cleaned up.  

There are cases when a single value might have multiple owners, in graph data structures, multiple edges might point to the same node, and that node is conceptually owned by all of the edges that point to it.  

##### Using Rc<T> to Share Data

Ony share data between multiple parts of your program for reading only.  

We can use `Rc<T>` due to `Rc:clone` only increments the reference count doesn't make a deep copy of all the data like most types' implementations of `clone` do.
And each time we call `clone`, the count goes up by 1, when `c` goes out of scope, the count goes down by 1, the implementation of the `Drop` trait decreases the reference count automatically when an `Rc<T>` value goes out of scope.  


### RefCell<T> and the Interior Mutability Pattern

`Interior mutability` is a design pattern in Rust that allows you to mutate data even when there are immutable references to that data. To mutable data, the pattern uses `unsafe` code inside the a data structure to bend Rust's usual rules that govern mutation and borrowing.  

##### Enforcing Borrowing Rules at Runtime with `RefCell<T>`

`RefCell<T>` type represents single ownership over the data it holds.  

The borrow rules:
* At any given time, you can have wither(but not both of) one mutable reference or any number of immutable references.
* Reference must always be valid.

Due to some analysis is impossible like: Halting Problem

* The `RefCell<T>` type is useful when you're sure your code follows the borrowing rules but the compiler is unable to understand and guarantee that

And `Rc<T>`, `RefCell<T>` is only for use in single-threaded scenarios and will give you a compile-time error if you try using it in a multithreaded context, (cp-16 will talk about)

#### Recap of the reasons to choose `Box<T>`, `Rc<T>`, or `RefCell<T>`
* `Rc<T>` enables multiple owners of the same data; `Box<T>` and `ReCell<T>` have single owners
* `Box<T>` allows immutable or mutable borrows checked at compile time;`Rc<T>` allows only immutable borrows checked at compile time
* `RefCell<T>` allows immutable or mutable borrows checked at runtime, because `Refcell<T>` allows mutable borrows checked at runtime, you can mutate the value inside the `RefCell<T>` even when the `RefCell<T>` is immutable
* Mutating the value inside an immutable value is the `interior mutability` pattern

#### Keeping Tack of Borrows at runtime with `RefCell<T>`

The `borrow` and `borrow_mut` methods are part of the safe API that belongs to `RefCell<T>`. The `borrow` method returns the smart pointer type `Ref<T>`, and the `borrow_mut` returns the sp type `RefMut<T>`. Both types implement `Deref`.  


### Reference cycles can leak memory
      
Rust allows memory leaks by using `Rc<T>` and `RefCell<T>`, it's possible to create references where items refer to each other in a cycle,this creates memory leaks because the reference count of each item in the cycle will never reach 0, and the values will never be dropped.
      
#### Preventing reference cycles

We've demonstrated that calling `Rc::clone` increases the `strong_count` of an `Rc<T>` instance, and an `Rc<T>` instance is only cleaned up if its `strong_count` is 0. And we can also create `weak reference` to the value within an `Rc<T>` instance by calling `Rc::downgrade` and passing a reference to the `Rc<T>`. The difference is the `weak_count` doesn't need to be 0 for the `Rc<T>` instance to be cleaned up.  

Strong reference are how you can share ownership of an `Rc<T>` instance, Weak references don't express an ownership relationship. And they don't cause reference cycle because any cycle involving some weak references will be broken once the strong reference count of values involved is 0.  

The function `upgrade` on `Weak<T>` instance help to check the value `Weak<T>` pointing to is exist.
