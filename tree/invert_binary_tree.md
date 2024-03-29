# Invert Binary Tree

> Invert a binary tree.

> ```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

> to

> ```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def invertTree(self, root):
        """
        :type root: TreeNode
        :rtype: TreeNode
        """
        if not root:
            return None
        self.invertTree(root.left)
        self.invertTree(root.right)
        root.left, root.right = root.right, root.left
        return root
```
