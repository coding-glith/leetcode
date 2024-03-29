# Balanced Binary Tree

> Given a binary tree, determine if it is height-balanced.

> For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        if abs(self.depth(root.left) - self.depth(root.right)) > 1:
            return False
        return self.isBalanced(root.left) and self.isBalanced(root.right)
    
    def depth(self, root):
        if not root:
            return 0
        return max(self.depth(root.left), self.depth(root.right)) + 1
```

The idea is to use the height of a tree as indicator. In the process of calculating the height of left and right subtree, compare its height, and return indicator or the height.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root == None:
            return True
        indicator = self.getHeight(root)
        if indicator != -1:
            return True
        else:
            return False

    def getHeight(self, root):
        if root == None:
            return 0
        left = self.getHeight(root.left)
        if left == -1:
            return -1
        right = self.getHeight(root.right)
        if right == -1:
            return -1
        heightDiff = abs(left - right)
        if heightDiff > 1:
            return -1
        else:
            return left + 1 if left > right else right + 1
```
