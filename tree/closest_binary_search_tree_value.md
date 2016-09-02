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

# Closest Binary Search Tree Value II

> Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

> Note:

> * Given target value is a floating point.

> * You may assume k is always valid, that is: k ≤ total nodes.

> * You are guaranteed to have only one unique set of k values in the BST that are closest to the target.

> Follow up:

> Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?

> Hint:

> * Consider implement these two helper functions:

>   * getPredecessor(N), which returns the next smaller node to N.

>   * getSuccessor(N), which returns the next larger node to N.

> * Try to assume that each node has a parent pointer, it makes the problem much easier.

> * Without parent pointer we just need to keep track of the path from the root to the current node using a stack.

> * You would need two stacks to track the path in finding predecessor and successor node separately.
