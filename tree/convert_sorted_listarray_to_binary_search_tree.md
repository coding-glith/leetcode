# Convert Sorted Array to Binary Search Tree

> Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

Binary search tree (BST) is a tree where for each node, the key of its left child is smaller than itself and the key of its right child is larger than itself. For a height balanced BST, the difference between heights of left subtree and right subtree is no more than 1.

```Python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if len(nums) == 0:
            return None
        mid =  len(nums) / 2
        root = TreeNode(nums[mid])  # put the middle number in the root
        root.left = self.arrayToBST(nums, 0, mid - 1)
        root.right = self.arrayToBST(nums, mid + 1, len(nums) - 1)
        return root

    def arrayToBST(self, nums, startIndx, endIndx):
        if startIndx > endIndx:
            return None
        midIndx = startIndx + (endIndx - startIndx) / 2
        root = TreeNode(nums[midIndx])
        root.left = self.arrayToBST(nums, startIndx, midIndx - 1)
        root.right = self.arrayToBST(nums, midIndx + 1, endIndx)
        return root
```

# Convert Sorted List to Binary Search Tree

> Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

```Python

```
