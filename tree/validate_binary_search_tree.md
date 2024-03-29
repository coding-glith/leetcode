# Validate Binary Search Tree

> Given a binary tree, determine if it is a valid binary search tree (BST).

> Assume a BST is defined as follows:

> * The left subtree of a node contains only nodes with keys less than the node's key.

> * The right subtree of a node contains only nodes with keys greater than the node's key.

> * Both the left and right subtrees must also be binary search trees.

> Example 1:

> ```
    2
   / \
  1   3
```

> Binary tree [2,1,3], return true.

> Example 2:

> ```
    1
   / \
  2   3
```

> Binary tree [1,2,3], return false.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.isBST(root, float('-inf'), float('inf'))

    def isBST(self, node, leftMax, rightMin):
        if node == None:
            return True
        if node.val <= leftMax or node.val >= rightMin:
            return False  # Once meet unsatisfied condition, return false. Otherwise continue recursion
        return self.isBST(node.left, leftMax, node.val) and self.isBST(node.right, node.val, rightMin)
```
