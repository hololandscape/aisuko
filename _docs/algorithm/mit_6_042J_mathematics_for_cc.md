---
title       : "Mathematics for CC"
excerpt     : "Mathematics for CC"
sitemap     : false
permalink   : /docs/mit_6_042J/
toc         : true
---

As I said before that in single-variable calculus. I will list the concepts only rather than the whole content of the course. I have checked all the materials. And according to my several years of experience in software(cloud) engineering. It looks like that many of the concepts from the mathematics for computer science are already known by myself.

There are still some `proofs` should be keep in mind.


## 2.6 Proofs about Sets

* Definitions of Sets
Informally, a `set` is a bunch of objects, which are called the elements of the set. The elements of s set can be just about anything: numbers, points in space, or even other sets. And there is no notion of an element appearing more than once in a set.


## 3 Induction (Powerful methods)

Although the three methods look and feel different, it turns out that they are equivalent in the sense that a proof using any one of the methods can be automatically reformatted so that it becomes a proof using any of the other methods.

* Well Ordering Principle
Every nonempty set of nonnegative integers has a smallest element.  
It is hard to see offhand why it is useful but ir provides one fo the most important proof rules in discrete mathematics.

* Induction Rule (Strong Induction)

I use it for so many years, I know what its name is now finally. This is the original I am trying to find always. 

<iframe src="https://hostux.social/@aisuko/109755347381853691/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

<iframe src="https://hostux.social/@aisuko/109755418614544189/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

* The difference between `Induction` and `Well Ordering`
Induction proofs are clearer because they resemble recursive procedures that reduce handling an input of size n+1 to handling one of size n. On the other hand, Well Ordering proofs sometimes seem more natural, and also come out slightly shorter.

* Is strong induction really "stronger" than ordinary induction?
It certainly looks that way, you just need to use a "stronger" induction hypothesis

### Structural Induction
The idea of induction is especially useful in connection with sets or data types that are defined recursively. And recursive data types play a central role in programming. Recursive definitions have two parts:

* Base case(s) that do not depend on anything else.
* Constructor case(s) that depend on previous cases.

