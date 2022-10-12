---
title       : "Data type VS Data structure"
excerpt     : "data type, structures"
sitemap     : false
permalink   : /docs/data_type_vs_data_structure/
toc         : true
---


## Data Type

> In computer science and computer programming, data type is a set of possible values and a set of allowed operations on it. A data type tells the compiler or interpreter how the programmer intends to use the data.

## Concept
A data type is a collection or grouping of data values. Such a grouping may be defined for many reasons: similarity, convenience, or to focus the attention.

## Data structures
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
  * Implementing a queue and it defined in Haskell as the ADT(Abstract data types)
  * Implementing the binary tree
    * allowing fast searching
    * can be defined in Haskell as the ADT

## Abstract data types
An abstract data type is a data type that does not specify the concrete representation of the data. Instead, a formal specification based on the data type's operations is used to describe it. Any implementation of a specification must fulfill the rules given.



## Reference

* https://en.wikipedia.org/wiki/Data_type
* https://en.wikipedia.org/wiki/Data_structure