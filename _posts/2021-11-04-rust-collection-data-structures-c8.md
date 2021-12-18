---
title: "Rust Collection Data Structures"
date: 2021-11-04T09:35
categories:
  - Summary
  - Document
tags:
  - rust
  - c8
---

The common collection data structures that the standard library provides:
* `vectors`
* `strings`
* `hash maps`

The `collections` is a data structures that can contain multiple values, these collections point to is stored on the heap which means the amount of data does not need to be known at compile time(but need to know what's types, and the types can help Rust know how much memory on the heap will be needed to store each element) and can grow or shrink as the program runs.

These three collections that are used very often in Rust programs:
* A `vector` allows you to store a variable number of values next to each other
* A `string` is a collection of characters
* A `hash map` allow you to associate a value with a particular key and it's a particular implementation of the more general data structure called a `map`


### Vector

Allow you to store more than one value in a single data structure that puts all the values next to each other in memory, and `Vector` can only store values of the same type, store the data on the `heap`.


__Properties__
* realistic way to create `vector` `Vec<T>`(`T` is a generic type)
  * use `vec!` macro for convenience
* updating a vector
  * use `push` method add elements to it  
* removing a vector
  * use `pop` method removes and return last element
* reading elements of vectors two ways to get the element are 
  * by using `&` and `[]` which gives us a reference: `let third: &i32=&v[2]`
  * by using the `get` method with the index passed as an argument,give us an `Option<&T>`

  ```
  match v.get(2){
      Some(third)=> println!("the third element is {}". third),
      None => println!("There is no third element."),
  }
  ```
* can't have mutable and immutable references in the same scopes


If we add new element to the end of the vector, the early borrowed element from the vector will not to be use, this is because the way vectors work adding a new element onto the end of the vector might require allocating new memory and copying the old elements to the new space, if there isn't enough room to put all the elements next to each other where the vector currently is the reference to the first element would be pointing to de-allocated memory.

using an enum to store multiple types
  * `vector` only can store same type values, so we can use `enum` to hold different values types and the all the enum variants will be considered the same type: that of the enum.



### Strings

Rust's propensity for exposing possible errors, string being a more complicated data structure than many programmers give them credit for, and UTF-8. `strings` are implemented as a collection of bytes.

* What's a String?
  * Rust has only one string type in the core language, is the string slice `str` that is usually seen in its borrowed from `&str`
  * String in Rust mean the `String` and the string slice `&str` types
  * `String` and string slice type and both of them are UTF-8 encoded
    
* Rust's standard library includes a number of other string types and they refer to owned and borrowed variants and can store text in different encoding or be represented in memory in a different way
  * `OsString`
  * `OsStr`
  * `CString`
  * `CStr`


__Properties__
* creating a new string
  * multiple ways and only is a matter of style

  ```
  let mut s=String::new();
  
  // to_string method can works on on any type implements the `Display` trait
  let data="initial contents";
  let s = data.to_string();
  
  // Use `String::from` and the code equivalent to above
  let s =String::from("initial contents");
  ```
* updating a string
  * `+` operator or `format!` macro to concatenate `String` values
* appending to a string with `push_str` and `push`
  * `push_str` take an string slice
  * `push` take a single character
* concatenation with the `+` operator or the `format!` Macro

`+` take the fist parameter ownership and the second parameter must be type reference of the `str(string slice)`, due to the `+` operator uses the `add` method and the method looks like.
  
  ```
  let s1=String::from("tic");
  let s2=String::from("link");

  let s3=s1+&s2;

  // the function that operator `+` in use
  fn add(self, s: &str) -> String {
  
  ```

**The reason that the code can compile, We + `&String` type not a `&str` type**

  * The `add` function can `coerce` the `&String` argument into a `&str` due to Rust uses a `deref coercion` the `&String` argument into a `&str`and that mean turns `&s2` into `&s2[..]`.
  * Add the `add` does not take ownership of the `s` parameter, `s2` will still be a valid `String` after this operation.
  * And `add` takes ownership of `self`, because `self` does not have an `&`. So, `s1` will be moved into the `add` call and no longer be valid after that.
  * So, `s3` is looks like will copy both strings and create a new one, thr statement actually takes ownership of `s1`, appends a copy of the contents of `s2`, and then return ownership to the result.
  * It implementation is more efficient than copying.

* `format!` is a Macro and does not take ownership of any of its parameters

* Rust strings don't support indexing e.g:`s[0]` (need to know how Rust stores strings in memory), because different letter encode in `UTF-8` will return different length
  * (three relevant ways to look at strings from Rust's perspective) for example `नमस्ते`
    * bytes
      * `[224, 164, 168, 224, 164, 174, 224]`
    * scalar values(`char` type in Rust)
    * show the word's under u8 values and contains their diacritic `['न', 'म', 'स', '्', 'त', 'े']`
        * grapheme clusters `["न", "म", "स्", "ते"]`

Rust provides different ways of interpreting the raw string data that computers store so each program can choose the interpretation it needs, although indexing operations are expected to always take constant time(O(1)), but it isn't possible to guarantee that performance with a `String`, because Rust would have to walk through the contents from the beginning to the index to determine how many valid characters there were.

We can use `[]` to create `string slice` 

* Methods for iterating over strings
  * by `charts()` return type `char` (scalar value)
  * by `bytes()` return raw type (bytes)
  * be sure to remember that valid Unicode scalar values may be made up of more than 1 byte getting grapheme clusters from strings is complex, so this functionality is not provided by the standard library, and the crates are available on [crates.io](https://crates.io/)


### Hash map

HashMap<K, V> store a mapping of keys of type K to values of type V, and use a different name, such as hash, map, object, hash table, dictionary or associative array, just to name a few.


**Creating a New Hash Map**

```
use std::collections:HashMap;

let mut scores =HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow", 50));
```


`HashMap` store their data on the heap, and all the `key` must have the same type, and all of the value must have the same type.


Another way to constructing a hash map is by using iterators and `collect` method on a vector of tuples

* `zip` method to create a vector of tuples
* insert reference to values into hash map, the values won't be moved into the hash map

```
use std::collections::HashMap;
let teams =vec![String::from("Blue"), String::from("Yellow")];
let initial_scores=vec![10, 50];

let mut scores: HashMap<_,_>=teams.into_iter().zip(initial_scores.into_iter()).collect();
```

`_` is default operator can match any value


__Properties__

Hash Maps and Ownership
* use `insert` add new elements
  * after `insert` the hash map will be the owner of those values
  * if `insert` references to values into the hash map, the values won't be moved into the hash map, and the values' `lifetime` must valid as long as the hash map

* accessing values in a hash map
  * `get` returns an `Option<&V>`, no value will return `None`

* Updating a Hash Map
  * it can replace the excited key
  * use the insert function to achieved `only inserting value if the key has no value`

```
// hash maps special API `entry` that takes the key you want to check as a parameter,return an `enum` called Entry represents a value that might or might not exist

scores.entry(String::from("Yellow")).or_insert(50);
```

`HashMap` uses a hashing function called `SipHash`, more security but not the fastest hashing algorithm.
