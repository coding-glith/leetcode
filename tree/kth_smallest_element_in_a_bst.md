# Kth Smallest Element in a BST

> Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

> Note: 

> You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

> Follow up:

> What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

> Hint:

> * Try to utilize the property of a BST.

> * What if you could modify the BST node's structure?

> * The optimal runtime complexity is O(height of BST).

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        count = self.countNodes(root.left)
        if k <= count:
            return self.kthSmallest(root.left, k)
        elif k > count + 1:
            return self.kthSmallest(root.right, k-1-count)
        return root.val

    def countNodes(self, root):
        if not root:
            return 0
        return self.countNodes(root.left) + self.countNodes(root.right) + 1
```
