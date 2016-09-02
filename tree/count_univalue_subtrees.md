# Count Univalue Subtrees

> Given a binary tree, count the number of uni-value subtrees.

> A Uni-value subtree means all nodes of the subtree have the same value.

> For example:

> Given binary tree,

> ```
              5
             / \
            1   5
           / \   \
          5   5   5
```

> return 4.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def countUnivalSubtrees(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.count = 0
        self.helper(root)
        return self.count

    def helper(self, root):
        if not root:
            return True
        left = self.helper(root.left)
        right = self.helper(root.right)
        if left and right and \
           (not root.left or root.left.val == root.val) and \
           (not root.right or root.right.val == root.val):
            self.count += 1
            return True
        return False
```
