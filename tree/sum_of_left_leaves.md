# Sum of Left Leaves

> Find the sum of all left leaves in a given binary tree.

> Example:

> ```
    3
   / \
  9  20
    /  \
   15   7
```

> There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

Recursive solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sumOfLeftLeaves(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root: return 0
        res = 0
        if root.left and not root.left.left and not root.left.right:
            res += root.left.val
        else:
            res += self.sumOfLeftLeaves(root.left)
        res += self.sumOfLeftLeaves(root.right)
        return res
```
