---
title       : "Introduction to Algorithms 02"
excerpt     : "Introduction to Algorithms 02"
sitemap     : false
permalink   : /docs/mit_6_006_02/
toc         : true
---

## Insertion sort

```python
###################################
# Operation 4: sort words into alphabetic order(inplace)
###################################
def insertion_sort(A):
    """
    Sort list A into order, in place and it uses 0-indexing
    """
    a_length=len(A)
    for j in range(a_length):
        key=A[j]
        i=j-1
        while i>-1 and A[i]>key:
            A[i+1]=A[i]
            i=i-1
        A[i+1]=key
    return A
```
