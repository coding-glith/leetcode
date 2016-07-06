# Flatten Binary Tree to Linked List

> Given a binary tree, flatten it to a linked list in-place.

> For example,

> Given

> ```
         1
        / \
       2   5
      / \   \
     3   4   6
```

> The flattened tree should look like:

> ```
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
```

Recursive: The idea here is to flatten the left child and right child, then link root with left child and right child.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        if root == None:
            return
        self.flatten(root.left)
        self.flatten(root.right)
        tmpNode = root
        if tmpNode.left == None:
            return
        tmpNode = tmpNode.left
        while tmpNode.right:
            tmpNode = tmpNode.right  # reach to the rightmost leaf
        tmpNode.right = root.right   # link right child to the rightmost of left child
        root.right = root.left
        root.left = None
```
