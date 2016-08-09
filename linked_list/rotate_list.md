# Rotate List

> Given a list, rotate the list to the right by k places, where k is non-negative.

> For example:

> Given 1->2->3->4->5->NULL and k = 2,

> return 4->5->1->2->3->NULL.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or not head.next or k <= 0:
            return head
        slow, fast, traverse = head, head, head
        # check the length of list
        len = 1
        while traverse.next:
            traverse = traverse.next
            len += 1
        print len
        while slow.next:
            for indx in xrange((k+1)%len):
                if fast.next:
                    fast = fast.next
                else:
                    fast = head
            slow = slow.next
        # fast is the prev node we need
        if fast == slow:
            return head
        prev = fast
        newHead = fast.next
        while fast.next:
            fast = fast.next
        fast.next = head
        prev.next = None
        return newHead
```
