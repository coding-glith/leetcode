# Maximum Depth of Binary Tree

> Given a binary tree, find its maximum depth.

> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        leftDepth = self.maxDepth(root.left)
        rightDepth = self.maxDepth(root.right)

        return max(leftDepth, rightDepth) + 1
```

# Minimum Depth of Binary Tree

> Given a binary tree, find its minimum depth.

> The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        return self.getDepth(root)

    def getDepth(self, root):
        if root is None:
            return sys.maxint
        if root.left is None and root.right is None:
            return 1
        return min(self.getDepth(root.left), self.getDepth(root.right)) + 1
```
