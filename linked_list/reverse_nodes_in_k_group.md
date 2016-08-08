# Reverse Nodes in k-Group

> Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

> If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

> You may not alter the values in the nodes, only nodes itself may be changed.

> Only constant memory is allowed.

> For example,

> Given this linked list: 1->2->3->4->5

> For k = 2, you should return: 2->1->4->3->5

> For k = 3, you should return: 3->2->1->4->5

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if k <= 1 or not head:
            return head
        dummy = ListNode(0)
        dummy.next = head
        p, prev = dummy, dummy

        while p:
            prev = p
            for indx in xrange(k):
                p = p.next
                if not p:
                    return dummy.next
            p = self.reverse(prev, p.next)
        return dummy.next
    
    def reverse(self, start, end):
        # return the last node of current list node
        p = start.next
        while p.next != end:
            n = p.next
            p.next = n.next
            n.next = start.next
            start.next = n
        return p
```
