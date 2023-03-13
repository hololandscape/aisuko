---
title: "The one for BST questions"                                        
categories:
  - bst
tags:
  - 
toc: True
toc_label: "Table of Contents"
toc_icon: "cog"
---

## The solutions for BST series problems

The questions are related to BST, `preorder`, `inorder`, `postorder` and `level-first` order are always useful function. Most of the basic level problems are using these knwoledge.
Others like counting the deepth of BST, check if symmetric Tree or binary tree are all need `Depth-First Search`. And make sure which strategy we should use at the program is most important.

### How to count the depth of BST?
We need to traverse every elements but how? So, the strategy should be the `Depth-First Search`. And the attributes of Binary Tree are very important too. 
But it is not the 100% same with `DFS`, we need to count the numbers of the loops. 

```python
depth=0
# we can also implement DFS by using queue because it is FIFO and we add element by order (root-left-right)
queue=[root]
while queue:
    # all the elements we need to travere
    i=len(queue)
    while i>0:
        node=queue.pop(0)
        if node.left:
	    queue.append(node.left)
        if node.right:
  	    queue.append(node.right)
        i-=1
    d+=1
return d

```


### How to validate a BST?
* The left subtree of a node contains only nodes with keys less than the node's key
* The right subtree of a node contains only nodes with keys greater than the node's key
* Both the left and right subtrees must also be BST

So, we need to make sure left<root<right, but how to make sure this? We need to have a preNode to keep the previous node's value and make sure it less than current node's value

```python
if not root:
    return root
pre=None
stack=[]
while True:
    # Common code for preOrder 
    while root:
        stack.append(root)
        root=root.left
    # all the elements have checked already
    if not stack:
        return True
    # check the node val from root-left-right
    node=stack.pop()
    if pre and pre.val>=node.val:
        return False
    pre=node
    root=node.right
```
