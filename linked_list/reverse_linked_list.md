# Reverse Linked List

> Reverse a singly linked list.

> Note: A linked list can be reversed either iteratively or recursively. Could you implement both?

Iteratively.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        while head:
            cur = head
            head = head.next
            cur.next = prev
            prev = cur
        return prev
```

Recursively.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        return self.reverse(head)

    def reverse(self, node, prev=None):
        if not node:
            return prev
        n = node.next
        node.next = prev
        return self.reverse(n, node)
```

# Reverse Linked List II

> Reverse a linked list from position m to n. Do it in-place and in one-pass.

> For example:

> Given 1->2->3->4->5->NULL, m = 2 and n = 4,

> return 1->4->3->2->5->NULL.

> Note:

> Given m, n satisfy the following condition:

> 1 ≤ m ≤ n ≤ length of list.

```Python

```
