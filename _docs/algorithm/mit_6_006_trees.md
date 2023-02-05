---
title       : "Trees"
excerpt     : "Trees"
sitemap     : false
permalink   : /docs/mit_6_006_03/
toc         : true
---

<iframe style="border-radius:12px" src="https://open.spotify.com/embed/track/1a4N2FIdBPUCwRkdrBYmkM?utm_source=generator" width="100%" height="152" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>

## Scheduling and Binary Search Trees

![full](https://hostux.social/system/media_attachments/files/109/782/705/366/615/843/original/ae5a74c8a3bc22a9.jpeg){: .full}

### Binary Search Trees

#### Properties
Each node x in the binary tree has a key key(x). Node other than the `root` have a parent p(x). Nodes may have a left child left(x) and/or a right child right(x). These are pointers unlike in a heap.(rooted binary tree)  
The invariant is: for any node x, for all nodes y in the left subtree of x, key(y) <=key(x). For all nodes y in the right subtree of x key(y)>=key(x).

#### Finding a value in the BST if it exists: find(val)
Follow left and right pointers until you find it ot hit NIL

#### Finding the minimum element in a BST:
Key is to just go left till you cannot go left anymore

#### Height of node
Length of longest downward path to a leaf

#### Complexity
All operations are O(h) where h is heigh of the BST, the algorithm for augmentation is as follows:
* Walk down tree to find desired node
* Add in nodes that are smaller
* Add in subtree sizes to the left

```python
# It needs to be implemented with python code
```

## Balanced BSTs
Why the binary search tree needs to be balanced?
* BSTs support insert, delete, min, max,next-larger, next-smaller, etc. in O(h) time, where h =height of tree(= height of root)
* h is between lg n and n
* balanced BST maintains h =O(lg n) -> all operations run in O(lg n) time

![image-right](https://hostux.social/system/media_attachments/files/109/783/342/841/625/848/original/901751ebf16841b4.jpeg){: .align-right}


## AVL Trees
Adel'son-Vel'skii & Landis 1962

![image-right](https://hostux.social/system/media_attachments/files/109/787/758/670/053/544/original/5e639fc161c20d6d.jpeg){: .align-right}

For every node, require heights of left & right children to differ by at most +1
* treat nil tree as height -1
* each node stores its height (DATA STRUCTURE AUGMENTATION) (like subtree size)(alternatively, can just store difference in heights)



![full](https://hostux.social/system/media_attachments/files/109/788/284/637/219/306/original/89be1cec6ada55cd.jpeg){: .full}

### AVL Insert
* Insert as in simple BST
* work your way up tree, restoring AVL property(And updating heights as you go)

![image-right](https://hostux.social/system/media_attachments/files/109/788/245/670/339/945/original/f87e1f4e7a30b894.jpeg){: .align-right}

![full](https://hostux.social/system/media_attachments/files/109/787/816/007/974/665/original/689905954540c7e8.jpeg){: .full}

![full](https://hostux.social/system/media_attachments/files/109/787/816/807/004/128/original/2de40a77de2b1373.jpeg){: .full}


## Big Picture
`Abstract Data Type(ADT)`: interface spec  
vs  
`Data Structure(DS)`: algorithm for each op  

There are many possible DSs for one ADT.

![full](https://hostux.social/system/media_attachments/files/109/788/402/173/926/513/original/d279c44ed8030be1.jpeg){: .full}



## Source
[https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/](https://ocw.mit.edu/courses/6-006-introduction-to-algorithms-fall-2011/pages/lecture-notes/)