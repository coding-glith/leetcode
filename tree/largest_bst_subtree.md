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

Not quite understand yet. :-(

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
        def dfs(root):
            if not root:
                return 0, 0, float('inf'), float('-inf')
            leftGlobal, leftLocal, min1, max1 = dfs(root.left)
            rightGlobal, rightLocal, min2, max2 = dfs(root.right)
            local = leftLocal + 1 + rightLocal if max1 < root.val < min2 else float('-inf')
            return max(leftGlobal, rightGlobal, local), local, min(min1, root.val), max(max2, root.val)
        return dfs(root)[0]
```
