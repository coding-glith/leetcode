# Inorder Successor in BST

> Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

> Note: If the given node has no in-order successor in the tree, return null.

First, understand inorder successor from explanations [here](http://www.geeksforgeeks.org/inorder-successor-in-binary-search-tree/). In Binary Tree, Inorder successor of a node is the next node in Inorder traversal of the Binary Tree.

```Python

```

This solution is first do inorder traversal, and store it in a list, then search for the node wanted. Need to go over the whole tree, not a ideal solution.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def inorderSuccessor(self, root, p):
        """
        :type root: TreeNode
        :type p: TreeNode
        :rtype: TreeNode
        """
        def helper(root, p, d):
            if not root:
                return
            helper(root.left, p, d)
            d.append(root)
            helper(root.right, p, d)
            
        d = []
        helper(root, p, d)
        for i, node in enumerate(d):
            if node == p and i < len(d)-1:
                return d[i+1].val
        return None
```
