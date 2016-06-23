# Same Tree

> Given two binary trees, write a function to check if they are equal or not.

> Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if p == None and q == None:
            return True
        if p == None or q == None:
            return False
        nodeBool = (p.val == q.val)
        leftBool = self.isSameTree(p.left, q.left)
        rightBool = self.isSameTree(p.right, q.right)
        return nodeBool and leftBool and rightBool
```
