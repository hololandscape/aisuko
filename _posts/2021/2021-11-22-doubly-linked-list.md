---
title: "Doubly Linked List"
date: 2021-11-22T18:46
categories:
  - Document
tags:
  - doubly-linked-list
  - data-structures
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---


What's mean of the Linked list's tail pointer?  

* Inserting at the end is O(1) instead of O(N)
* In a Doubly Linked List then removing from the end is also O(1) instead of O(N)

And the pointer will takes up a trivial amount of extra memory.  

If we design a doubly linked list, add the `self.tail` pointer would be good. Because the pointer can support us on `add` or `delete` by the index operations when the index equals to length of linked list.  

[Design Linked List](https://leetcode.com/explore/learn/card/linked-list/210/doubly-linked-list/1294/)

## Persistent data structure

In computing a persistent data structure or not ephemeral data structure is a data structure that always preserves the previous version of itself when it is modified. Such data structures are effectively immutable, as their operations do not visibly update the structure in-place, but instead always yield a new updated structure.

__Reference__

[SoftwareEngineer](https://softwareengineering.stackexchange.com/questions/301862/should-linked-lists-always-have-a-tail-pointer)
[Persistent data structure](https://en.wikipedia.org/wiki/Persistent_data_structure)
[The Algorithms Python](https://github.com/Aisuko/Python/tree/master/data_structures/linked_list)
