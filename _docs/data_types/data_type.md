---
title       : "Data type"
excerpt     : "data type"
sitemap     : false
permalink   : /docs/data_type/
toc         : true
---


## Data Type
> In computer science and computer programming, data type is a set of possible values and a set of allowed operations on it. A data type tells the compiler or interpreter how the programmer intends to use the data.


## Concept
> A data type is a collection or grouping of data values. Such a grouping may be defined for many reasons: similarity, convenience, or to focus the attention.

* Primitive types
* Composite types or non-primitive type
* Abstract data types


## Notable data types

### Machine data types

All data based on digital electronics is represented a bits on the lowest level.

### Boolean type

Represents the true and false.

### Numeric types

Integer data types.

### Enumerations

The enumerated type has distinct values, which can be compared and assigned, but which do not necessarily have any particular concrete representation in the computer's memory.

### String and text types

Strings are a sequence of characters used to store words or plain text, most often textual markup languages representing formatted text.

### Union types

A tagged union(also called a variant) contains an additional field indicating its current type for enhanced type safety.

### Algebraic data types

An ADT is a possibly recursive sum type of product types.

### Data structures

Some types are very useful for storing and retrieving data and are called data structures. Common data structures include:

* An array(also called vector, list or sequence) stores a number of elements and provides `random access` to individual elements.
  * Typically required to be the same type
  * May be fixed-length or expandable
  * Indices into an array are typically required to be integers

* Record(also called tuple or struct)
  * simplest
  * typically indexed by names
  * typically in fixed number and sequence

* An object contains a number of data fields, like record, and also a number of subroutines for accessing or modifying them, called methods

* Singly linked list
  * Implementing a `queue` and it defined in Haskell as the ADT(Abstract data types)

* Binary tree
    * allowing `fast searching`
    * can be defined in Haskell as the ADT

### Abstract data types
An abstract data type is a data type that does not specify the concrete representation of the data. Instead, a formal specification based on the data type's operations is used to describe it. Any implementation of a specification must fulfill the rules given.

### Pointers and references

A data type whose value refers directly to another values stored elsewhere in the computer memory using its address. If the value of pointer was never a valid memory address would cause a program to crash. This is an potential problem.


### Others
* Function types
* Type constructors
* Quantified types
* Refinement types
* Dependent types
* Meta types
* Convenience types


## Source
* [https://en.wikipedia.org/wiki/Data_type](https://en.wikipedia.org/wiki/Data_type)
* [https://en.wikipedia.org/wiki/Data_structure](https://en.wikipedia.org/wiki/Data_structure)







