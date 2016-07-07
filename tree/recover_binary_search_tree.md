# Recover Binary Search Tree

> Two elements of a binary search tree (BST) are swapped by mistake.

> Recover the tree without changing its structure.

> Note:

> A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

This solution is based on in-order traversal, it's not the O(n) space solution - needs Morris Traversal. The idea here is use in-order traversal to find out the wrongly placed nodes, and store them in two variables: first/second. After find out the two nodes, swap them.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def __init__(self):
        self.first = None
        self.second = None   # store two wrongly placed nodes
        self.prev = TreeNode(float('-inf'))
    
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        self.traverse(root)
        
        # swap the value of the first and second node
        tmp = self.first.val
        self.first.val = self.second.val
        self.second.val = tmp
    
    def traverse(self, root):
        if root == None:
            return
        # in-order traversal
        self.traverse(root.left)
        if self.first == None and self.prev.val >= root.val:
            # prev represents the left subtree, the value should be smaller than root
            self.first = self.prev
        if self.first != None and self.prev.val >= root.val:
            # for the second wrong node, it should be the smaller one, because we anticipate the root to be larger
            self.second = root
        self.prev = root  # prev is the previous node during this in-order traversal
        self.traverse(root.right)
```
