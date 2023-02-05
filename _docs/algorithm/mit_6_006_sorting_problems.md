---
title       : "Sorting Problems"
excerpt     : "Sorting Problems"
sitemap     : false
permalink   : /docs/mit_6_006_04/
toc         : true
---


<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/1FGvbfMafLBdymgrtGAZYh?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

### Linear-Time Sorting Overview
* Comparison model
* Lower bounds in the comparison model
  - searching: binary search, AVL tree search optimal 
    ```markdown
    $\Omega(lg n)$
    ```
  - sorting: merge sort, heap sort, AVL sort optimal
    ```markdown
    $\Omega(n lg n)$
    ```
* O(n) sorting algorithms for small integers
  - counting sort
  - radix sort

### Comparison Model of Computation
* input items are ADTs
* only support comparisons(<,>,<=, etc)
* time cost =# comparisons

### Decision Tree
Any comparison algorithm can be viewed/specified as a tree of all possible comparison outcomes&resulting output, for a particular n, e.g: n=3
![full](https://hostux.social/system/media_attachments/files/109/792/412/686/129/682/original/d5cbbddf2d8ef7ce.jpeg){: .full}

#### Search Lower Bound
* \# leaves >= \# possible answers >=n
* decision tree is binary
* ==> height >= $lgn+-\\Theta(1)$

#### Sorting Lower bound
* leaf specifies as permutation: A[3]<=A[1]<=A[9]<=...
* all n! are possible answer
* \# leaves >=n! ==> $\\Omega(nlgn)$

#### Linear-time Sorting
If n keys are integers,
    * ==> lower bounds do not apply
    * if $k=\mathrm{n}^{O(1)}$, can sort in O(n) time

#### Counting Sort
Time: $\\Theta(n+k)$; also $\\Theta(n+k)$ space
![image-left](https://hostux.social/system/media_attachments/files/109/792/525/563/444/839/original/05ed5d0a71d4215a.jpeg){: .aligen-left}

#### About Radix Soft 
![full](https://hostux.social/system/media_attachments/files/109/792/564/978/371/751/original/e38c2de5f9218910.jpeg)


## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)