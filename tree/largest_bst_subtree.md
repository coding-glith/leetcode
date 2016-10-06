# Largest BST Subtree

> Given a binary tree, find the largest subtree which is a Binary Search Tree (BST), where largest means subtree with largest number of nodes in it.

> Note:

> A subtree must include all of its descendants.

> Here's an example:

> ```
    10
    / \
   5  15
  / \   \ 
 1   8   7
```

> The Largest BST Subtree in this case is the highlighted one. 

> The return value is the subtree's size, which is 3.

> Follow up:

> Can you figure out ways to solve it with O(n) time complexity?

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def largestBSTSubtree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return self.getSub(root)[0]

    def getSub(self, root):
        if not root:
            return 0, 0, sys.maxint, -sys.maxint-1
        leftRes, leftCount, leftmin, leftmax = self.getSub(root.left)
        rightRes, rightCount, rightmin, rightmax = self.getSub(root.right)
        if root.val > leftmax and root.val < rightmin:
            count = leftCount + rightCount + 1
        else: count = -sys.maxint - 1   # for below[0] will not return this if don't satisfy above condition
        return max(leftRes, rightRes, count), count, min(leftmin, root.val), max(rightmax, root.val)
```
