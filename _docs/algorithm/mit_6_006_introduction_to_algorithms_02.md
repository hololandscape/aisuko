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

Insertion sort  
Running time: O(n^2) because O(n^2) compares and O(n^2) swaps e.g. when input is A=[n,...,2,1]

Binary Insertion sort  
It will take O(log n) time. However, shifting the elements after insertion will still take O(n) time  
Complexity: O(n log n) comparisons,  n^2 swaps

Merge soft (Key subroutine: Merge)  
If `n=1`, done(nothing to sort). Otherwise, recursively sort A[1..n/2] and A[n/2+1..n]. "Merge" the two sorted sub-arrays  
Running time = O(n) to merge a total of n elements (linear time)
