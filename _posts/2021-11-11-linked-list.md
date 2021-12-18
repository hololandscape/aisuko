---
title: "Linked List"
date: 2021-11-11T14:07
categories:
  - Summary
  - Document
tags:
  - data-structure
  - linked-list
---

Similar to the array, the linked list is also a `linear` data structure. And each element in the linked list is actually a separate object while all the objects are `linked together by the reference field` in each element.

There are two types of linked list: `singly linked list` and `doubly linked list`.

## The skills for Linked list
* Structure of singly linked list and doubly linked list;
* Implement traversal, insertion, deletion in a singly or doubly linked list;
* Analyze the complexity of different operations;
* Two-pointer technique in the linked list;
* Solve the classic problems such as reverse a linked list;


## Singly Linked List

Each node contains not only the value but also `a reference field` to link to the next node.


### Node Structure

We use the head node `head` to represent the whole list.

```python
from typing import Any

class Node:
    def __init__(self, data: Any):
        self.data=data
        self.next=None
    
    def __repr__(self)-> str:
        return f"Node({self.data})"
```

### Operations

We are not able tp access a random element in a singly-linked list in constant time. If we want get the ith element, we have to traverse from the head node one by one. It takes `O(N)` time on average to `visit an element by index`, where N is the length of the linked list.  


#### Add

* unlike an array, we don't need to move all elements past the inserted element.
  * new value
  * linked the "next" field of new value to prev's next node
  * link the "next" field in `prev` to the new value

* `addAtHead O(1)` add a node at the beginning
  * we use the head node `head` to represent the whole list, so it is essential to update `head` when adding a new node at the beginning of the list.
  * initialize a new node `cur`
  * lind the new node to our original head node `head`
  * assign `cur` to `head`

* `addAtTail(int val) O(n)` append a node as the last element of the linked list
  * we get the head node
  * iterator the linked-list to get the node in the end or the specify node(index)
  * replace the `node.next` equal to the new node

* `addAtIndex(int index, int val)` 
  * add a node of value before the `index` node in the linked list. `O(index-1)`
  * If `index` equals the length of the linked list, the node will be append to the end of the linked list. `O(n) n=len(linked_list)`
  * If `index` is greater than the length, the node will not be inserted


#### Delete

* delete the node `cur` can do it in two steps `O(index)`
  * find cur's previous node `prev` and its next node `next`;
  * link `prev` to cur's node next
  * 

It is easy to find out `next` using the reference field of `cur`. However, we have to traverse the linked list from the head node to find out `prev` which will take O(N) time on average, N is the length of the linked list.  

The space complexity is `O(1)` because we only need constant space to store our pointers.

* delete the first node
  * assign the next node too head

* delete the last node
  * we get the head node
  * iterator the whole linked-list in order to get the node in the end
  * let the node ahead of the last node as the last node `node.next=node.next.next`

#### Traverse

* we can implement iterator to support traverse

```python
def __iter__(self) -> Any:
    node=self.head
    while node:
        yield node.data
        node=node.next
```

#### Implement Linked-List

[Single linked list](https://github.com/hololandscape/sicp/blob/main/python/data_structures/linked_list/single_linkerd_list.py)

 ### __Source to read:__
* [Coding-interview-university](https://github.com/jwasham/coding-interview-university)  
* [TheAlgorithms](https://github.com/TheAlgorithms/Python)
* [LeetCode](https://leetcode.com/explore/learn/card/linked-list/209/singly-linked-list/1290/)