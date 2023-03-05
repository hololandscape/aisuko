---
title       : "Basics of Rust Concurrency"
excerpt     : "Basics of Rust Concurrency"
sitemap     : false
permalink   : /docs/basic_of_concurrency_rust/
toc         : true
---

## Threads in Rust
* `threads`
* `interior mutability`
* `Send` and `Sync`
* `mutex`
* `a condition variable`
* `thread parking` 

### Create threads
Two ways to create new threads:

* `std::thread::spawn`

```rust
fn main(){
    let t1=thread:spawn(f);
    let t2=thread::spawn(f);

    println!("Hello from the main thread.");

    t1.join().unwrap();
    t2.join().unwrap();

    }
```

* use `closure`, it allows us to capture values to move into the thread
Borrowing data from longer-living parent threads

```rust
let numbers = Vec::from_iter(0..=100);
// transferring ownership of a value to a thread
let t =thread::spawn(move || {
    let len=numbers.len();
    let sum=numbers.iter().sum::<usize>();
    sum/len
});
// if average had been empty, the thread would have panicked while trying to divide by zero
let average=t.join().unwrap();
println!("average: {average}");
```

### Scoped Threads
It allows us to spawn threads that cannot outlive the scope of the closure to safely borrow local variables.

```rust
// when the scope ends, all threads that haven't been joined yet are automatically joined.
let numbers=vec![1,2,3];
// After 1.63 it was already updated
thread::scope(|s| {
    s.spawn(|| {
        println!("length: {}", numbers.len());
    });
    s.spawn(|| {
        for n in &numbers{
            println!("{n}");
        }
    });
});
```

#### Output Locking
`println` macro uses `std::io::Stdout::lock()` make sure its output does not get interrupted.

#### The Leakpocalypse
The design of a safe interface cannot rely on the assumption that objects will always be dropped at the ned of their lifetime.

`std::mem::forget` as a safe function from Rust 1.0 to emphasize that forgetting (or leaking ) is always a possibility.

### Shared Ownership and Reference Counting
Many ways to create variables that is not owned by a single thread

#### Statics
`'static` lifetime does not mean that value lived since the start of the program, but only that it lives to the end of the program

```rust
static X: [i32; 3]=[1,2,3]
```

#### Leaking
The downside of leaking a Box is that we are leaking memory
```rust
let x: &'static [i32; 3]=Box::leak(Box::new([1,2,3]));
```

#### Reference Counting
To make sure that shared data gets dropped and deallocated we can share ownership.

* `std::rc::Rc` very similar to a box, except it will not allocate anything new, but instead increment a counter stored next the contained value.
* Dropping an Rc will decrement the counter. Only the last Rc, which will see the counter drop to zero.
* Rc is not thread safe

#### Atomically reference counted
It guarantees that modifications to the reference counter are indivisible atomic operations, making it safe to use it with multiple threads.

* `std::sync::Arc`

### Borrowing and Data Races
In order to prevent data races, values can be borrowed in two ways:
* immutable borrowing
* Mutable borrowing

Using an unsafe block to disable some of the compiler's safely checks.

#TODO

### Reference:
https://marabos.nl/atomics/basics.html