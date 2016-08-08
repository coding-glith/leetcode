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
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

The idea is to find m then swap one by one from m to n.

class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if not head:
            return head

        dummy = ListNode(0)
        dummy.next = head
        p = dummy
        for indx in xrange(1, m):
            p = p.next
        # currently, p is the prevNode of m
        mNode = p.next
        for indx in xrange(m, n):
            nNode = mNode.next
            mNode.next = nNode.next
            nNode.next = p.next
            p.next = nNode
        return dummy.next
```
