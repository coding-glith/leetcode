# Count Complete Tree Nodes

> Given a complete binary tree, count the number of nodes.

> Definition of a complete binary tree from Wikipedia:

> In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

Count one by one is slow. The maximum number of nodes in a binary tree is 1+2+...+2^h = 2^(k+1)-1. Check the height of root's left and right subtree, if height is the same, then count 2^k-1+1 = 2^k and go right.

Iterative solution.

```Python
class Solution(object):
    def countNodes(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        count = 0
        while root:
            left, right = map(self.height, (root.left, root.right))
            if left == right:
                count += 2 ** left
                root = root.right
            else:
                count += 2 ** right
                root = root.left
        return count

    def height(self, root):
        # O(log(n))
        h = 0
        while root:
            h += 1
            root = root.left
        return h
```

Recursive solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def countNodes(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        h = self.height(root)
        if h < 0:
            return 0
        else:
            if self.height(root.right) == h - 1:
                return 2 ** h + self.countNodes(root.right)
            else:
                return 2 ** (h - 1) + self.countNodes(root.left)

    def height(self, root):
        # O(log(n))
        return -1 if not root else 1 + self.height(root.left)
```
