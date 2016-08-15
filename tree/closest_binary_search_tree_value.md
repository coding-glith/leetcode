# Closest Binary Search Tree Value

> Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

> Note:

> * Given target value is a floating point.

> * You are guaranteed to have only one unique value in the BST that is closest to the target.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def closestValue(self, root, target):
        """
        :type root: TreeNode
        :type target: float
        :rtype: int
        """
        parentVal = root.val
        child = root.left if target < parentVal else root.right
        if not child:
            return parentVal
        childVal = self.closestValue(child, target)
        return childVal if abs(target - childVal) < abs(target - parentVal) else parentVal
```
