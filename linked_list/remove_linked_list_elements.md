# Remove Linked List Elements

> Remove all elements from a linked list of integers that have value val.

> Example

> Given: 1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, val = 6

> Return: 1 --> 2 --> 3 --> 4 --> 5

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        if not head:
            return head
        dummy = ListNode(0)
        dummy.next = head
        p = dummy
        while p.next:
            if p.next.val == val:
                p.next = p.next.next
            else:
                p = p.next
        return dummy.next
```
