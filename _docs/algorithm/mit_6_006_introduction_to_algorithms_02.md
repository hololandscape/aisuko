---
title       : "Introduction to Algorithms 02"
excerpt     : "Introduction to Algorithms 02"
sitemap     : false
permalink   : /docs/mit_6_006_02/
toc         : true
---

## The problem of sorting
Problems that become easy once items are in sorted order
* Find a median, or find closest paris
* Binary search, identify statistical outliers

Non-obvious applications
* Data compression: sorting finds duplicates
* Computer graphics: rendering scenes front to back

### Insertion sort  
Running time: O(n^2) because O(n^2) compares and O(n^2) swaps e.g. when input is A=[n,...,2,1]

### Binary Insertion sort  
It will take O(log n) time. However, shifting the elements after insertion will still take O(n) time  
Complexity: O(n log n) comparisons,  n^2 swaps

### Merge soft (Key subroutine: Merge)  
If `n=1`, done(nothing to sort). Otherwise, recursively sort A[1..n/2] and A[n/2+1..n]. "Merge" the two sorted sub-arrays  
Running time = O(n) to merge a total of n elements (linear time)

### Heap-Sort
Sorting Strategy:
* Build Max Heap from unordered array;
* Find maximum element `A[l]`;
* Swap elements A[n] and A[l]; now max element is at the end of the array
* Discard node n from heap(by decrementing heap-size variable)
* New root may violate max heap property, but its children are max heaps. Run `max_heapify` to fix this
* Go to Step 2 unless heap is empty

Running time
After n iterations the Heap is empty every iteration involves `a swap` and a `max_heapify operation`; hence it takes O(log n) time. Overall O(n log n)

## Data structures
<iframe src="https://hostux.social/@aisuko/109781364506786788/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="700" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

<iframe src="https://hostux.social/@aisuko/109781962045878255/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="400" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

Heap Operations
`build_max_help` produce a max-heap from an unordered array
`max_heapify` correct a single violation of the heap property in a subtree at its root
`insert, extract_max, heapsort`

Max_heapify with O(log n)
Assume that the trees rooted at left(i) and right(i) are max-heaps

```python
# max_Heapify Pseudocide
l=left(i)
r=right(i)
if(l<=heap_size(A) and A[l]>A[i])
    largest =l
else
    largest=i
if (r<=heap-size(A) and A[r]>A[largest])
    largest=r
if largest !=i:
    exchange A[i] and A[largest]
# Max_Heapify(A, largest)
```

<iframe src="https://hostux.social/@aisuko/109782285623362932/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="600" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

