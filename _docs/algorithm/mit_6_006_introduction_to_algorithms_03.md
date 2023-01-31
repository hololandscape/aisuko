---
title       : "Introduction to Algorithms 03"
excerpt     : "Introduction to Algorithms 03"
sitemap     : false
permalink   : /docs/mit_6_006_03/
toc         : true
---


## Scheduling and Binary Search Trees
<iframe src="https://hostux.social/@aisuko/109782731343121919/embed" class="mastodon-embed" style="max-width: 100%; border: 0" width="700" allowfullscreen="allowfullscreen"></iframe><script src="https://hostux.social/embed.js" async="async"></script>

### Binary Search Trees
Properties
Each node x in the binary tree has a key key(x). Node other than the root have a parent p(x). Nodes may have a left child left(x) and/or a right child right(x). These are pointers unlike in a heap.  
The invariant is: for any node x, for all nodes y in the left subtree of x, key(y) <=key(x). For all nodes y in the right subtree of x key(y)>=key(x).

Finding a value in the BST if it exists: find(val)
Follow left and right pointers until you find it ot hit NIL

Finding the minimum element in a BST:
Key is to just go left till you cannot go left anymore

Complexity
All operations are O(h) where h is heigh of the BST, the algorithm for augmentation is as follows:
* Walk down tree to find desired node
* Add in nodes that are smaller
* Add in subtree sizes to the left

### Balanced BSTs




## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)