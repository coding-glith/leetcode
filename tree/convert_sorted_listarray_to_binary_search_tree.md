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
        return self.arrayToBST(nums, 0, len(nums) - 1)

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

The hard part here is to get the middle point of the list. Here, we use two pointers, everytime 'slow' will move one step while 'fast' move two steps. So when 'fast' reaches to the end of the list, 'slow' will be at the middle of the list. 

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if not head:
            return None
        return self.listToBST(head, None)

    def listToBST(self, head, tail):
        if head == tail:
            return None
        slow, fast = head, head   # use fast/slow pointers to get the mid node of list
        while fast != tail and fast.next != tail:
            slow = slow.next
            fast = fast.next.next
        root = TreeNode(slow.val)
        root.left = self.listToBST(head, slow)
        root.right = self.listToBST(slow.next, tail)
        return root
```
