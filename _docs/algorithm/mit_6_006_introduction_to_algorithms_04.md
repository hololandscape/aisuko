---
title       : "Introduction to Algorithms 04"
excerpt     : "Introduction to Algorithms 04"
sitemap     : false
permalink   : /docs/mit_6_006_04/
toc         : true
---


### Linear-Time Sorting Overview
* Comparison model
* Lower bounds in the comparison model
  - searching: $&#92;&#92;Omega(lg n)$
    * binary search, AVL tree search optimal
  - sorting: $&#92;&#92;Omega(n lg n)$
    * mergesort, heap sort, AVL sort optimal
* O(n) sorting algorithms for small integers
  - counting sort
  - radix sort
### Comparison Model of Computation
* input items are ADTs
* only support comparisons(<,>,<=, etc)
* time cost =# comparisons
### Decision Tree
Any comparison algorithm can be viewd/specified as a tree of all possible comparison outcomes&resulting output, for a particular n, e.g: n=3
<iframe src="https://hostux.social/@aisuko/109792413791655680/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="600" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

#### Search Lower Bound
* /\# leaves >= /# possible answers >=n
* decision tree is binary
* ==> height >= $lg n+-\Theta(1)$
#### Sorting Lower bound
* leaf specifies as permutaion: A[3]<=A[1]<=A[9]<=...
* all n! are possible answer
* \# leaves >=n! ==> $\Omega(nlgn)$
#### Linear-time Sorting
If n keys are integers,
* ==> lower bounds do not apply
* if $k=\mathrm{n}^{O(1)}$, can sort in O(n) time
#### Counting Sort
Time: $\Theta(n+k)$ also $\Theta(n+k) space$
<iframe src="https://hostux.social/@aisuko/109792527021576313/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="600" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

#### Radix Soft

![full](https://hostux.social/system/media_attachments/files/109/792/564/978/371/751/original/e38c2de5f9218910.jpeg)

<!-- <iframe src="https://hostux.social/@aisuko/109792566034413931/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="600" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script> -->


## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)