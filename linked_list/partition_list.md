# Partition List

> Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

> You should preserve the original relative order of the nodes in each of the two partitions.

> For example,

> Given 1->4->3->2->5->2 and x = 3,

> return 1->2->2->4->3->5.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        psmall = ListNode(0)
        plarge = ListNode(0)
        ps, pl, p = psmall, plarge, head
        while p:
            if p.val < x:
                ps.next = p
                ps = ps.next
            else:
                pl.next = p
                pl = pl.next
            p = p.next
        pl.next = None  # must set the end of the list
        ps.next = plarge.next
        return psmall.next
```
