# Swap Nodes in Pairs

> Given a linked list, swap every two adjacent nodes and return its head.

> For example,

> Given 1->2->3->4, you should return the list as 2->1->4->3.

> Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        dummy = ListNode(0)
        dummy.next = head
        p, prev = dummy, dummy
        while p.next and p.next.next:
            p = p.next
            secNode = p.next
            p.next = secNode.next
            secNode.next = prev.next
            prev.next = secNode
            prev = p
            
        return dummy.next
```
