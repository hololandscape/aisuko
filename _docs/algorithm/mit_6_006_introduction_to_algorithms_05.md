---
title       : "Introduction to Algorithms 05"
excerpt     : "Introduction to Algorithms 05"
sitemap     : false
permalink   : /docs/mit_6_006_05/
toc         : true
---


## Hashing
### Dictionary problem
ADT- maintain a set of items, each with a key
* insert(item)
* delete(item)
* search(key)
Balanced BSTs solve in O(lg n) time per op. But our goal is O(1) time per op.
### Motivation
* compilers & interpreters: name -> variables
* network routers: IP address -> wire
* network server: port number -> socket/app
* virtual memory: virtual address -> physical
### Hashing function for dictionary problem
#### Simple Approach: Direct Access Table
The items would need to be stored in an array, indexed by key(random access)
##### Problems:
* keys must be nonnegative integers(or using two array, integers)
* large key range => large space - e.g one key of $\mathrm{2}^{256}$
##### Solution
* `prehash` key to integers, e.g: has(obj) in Python
* hashing
  * Reduce universe U of all keys down to reasonable size m for table
  * idea: m(above=)n
  * hash function h
![full](https://hostux.social/system/media_attachments/files/109/800/480/340/792/879/original/95403eabfe166740.jpeg){: .full}
##### How to deal with collisions?
##### Chaining
* Search must go through whole list T[h(key)]
* The worst case is $\Theta (n)$
Linked list of colliding elements in each slot of table
![full](https://hostux.social/system/media_attachments/files/109/800/480/340/792/879/original/95403eabfe166740.jpeg){: .full}
##### Open addressing
![full](https://hostux.social/system/media_attachments/files/109/803/822/580/949/145/original/872b52b688a45ca1.jpeg){: .full}
##### Simple Uniform Hashing
Each key is equally likely to be hashed to any slot of table, independent of where other keys are hashed.  
Performance
* The expected running time for search is $\mathrm(1+\alpha)$, the 1 comes from applying the hash function and random access to the slot whereas the $\alpha$ comes from searching the list.
### Hash Functions
Three methods to achieve the above performance:
* Division Method
  * It is inconvenient to find a prime number, and division is slow.
  ```
  h(k)=k mod m
  ```
* Multiplication Method
  * It is faster than division. m =table size = $\mathrc 2^r$
* Universal Hashing
  * It as good as Multiplication Method and Division Method

### Open Addressing vs Chaining
Open Addressing: better cache performance(better memory usage, no pointers needed)
Chaining: less sensitive to hash functions

### Desirable Properties
* One way(OW)
* Collision-resistance(CR)
* Target collision-resistance(TCR)
TCR is weak than CR. If a hash function satisfies CR, it automatically satisfies TCR. There is no implication relationship between OW and CR/TCR.


## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)