---
title       : "Mathematics for CC"
excerpt     : "Mathematics for CC"
sitemap     : false
permalink   : /docs/mit_6_042J/
toc         : true
---

As I said before that in single-variable calculus. I will list the concepts only rather than the whole content of the course. I have checked all the materials. And according to my several years of experience in software(cloud) engineering. It looks like that many of the concepts from the mathematics for computer science are already known by myself.



## 2.6 Proofs about Sets
There are still some `proofs` should be keep in mind.

Definitions of Sets: Informally, a `set` is a bunch of objects, which are called the elements of the set. The elements of s set can be just about anything: numbers, points in space, or even other sets. And there is no notion of an element appearing more than once in a set.


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

### 3.5 Structural Induction
The idea of induction is especially useful in connection with sets or data types that are defined recursively. And recursive data types play a central role in programming. Recursive definitions have two parts:

* Base case(s) that do not depend on anything else.
* Constructor case(s) that depend on previous cases.

<iframe src="https://hostux.social/@aisuko/109758384909075609/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>


### 4 Number Theory
In 1977 highly secure cryptosystem(RSA) based on number theory was proposed.

<iframe src="https://hostux.social/@aisuko/109758531449354566/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>


### 5 Structure
The better you can understand the structure, the better your results will be. The most important structure is computer science is a graph, also known as a `network`.

<iframe src="https://hostux.social/@aisuko/109758617989350531/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

#### 5.7 Trees
Graphs without cycles (called acyclic graphs) are probably the most important graphs of all when it comes to computer science.

* Definition 5.7.1. A connected acyclic graph is called a tree.
* Definition 5.7.2. If every connected component of a graph G is a tree, then G is a forest.
* Definition 5.7.3. A leaf is a node with degree 1 in a tree(or forest)

* Theorem 5.7.4. Every tree has the following properties:
  * 1. Any connected subgraph is a tree.
  * 2. There is a unique simple path between every pair of vertices.
  * 3. Adding an edge between nonadjacent nodes in a tree creates a graph with a cycle.
  * 4. Removing any edge disconnects the graph
  * 5. If the tree has at least two vertices, then it has at least two leaves.
  * 6. The number of vertices in a tree is one larger than the number of edges.

#### 5.8 Planar Graphs
A planar graph is a graph that has a planar drawing.


### 6 Directed Graphs
A directed edge is an edge where the endpoint are distinguished-one is the head and one is the tail.
A graph with directed edges is called a directed graph or digraph.

* 6.1 Degrees
  * With directed graphs, the notion of degree splits into `indegree` and `outdegree`.

* 6.1.2 Directed Walks, Paths, and Cycles
  * A directed walk (or more simply, a walk) in a directed graph G is a sequence of vertices v0~vn and edges.
  * A directed path (or path) in a directed graph is walk where the nodes in the walk are all different.
  * A directed cycle (or cycle) in a directed graph is a closed walk where all the vertices vi are different for 0<=i<=k.

* 6.1.4 DAGs
  * If an undirected graph does not have any cycles, then it is a tree or a forest.
  * Definition 6.1.4
    * A directed graph is called a directed acyclic graph(or, DAG) it it does not contain any directed cycles.

## 10 Recurrences
A recurrence describes a sequence of numbers. And two big classes of recurrences, linear and divide-and-conquer.

### 10.2 Merge sort
  * If the input is a single number, then the algorithm does nothing, because the list is already sorted.
  * Otherwise, the list contains two or more numbers. The first half and the second half of the list are each sorted recursively. Them the two halves are merged to form a sorted list with all n numbers.
  * The maximum number of comparisons used in sorting n items is taken as an estimate of the running time.

* Two techniques are used to solve recurrences
  * guess-and-verify
  * plug-and-chug
  * These methods require spotting a pattern in sequence of numbers or expressions

### 10.3 Linear Recurrences

You just follow the recipe and get the answer






