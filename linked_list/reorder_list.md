# Reorder List

> Given a singly linked list L: L0→L1→…→Ln-1→Ln,

> reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

> You must do this in-place without altering the nodes' values.

> For example,

> Given {1,2,3,4}, reorder it to {1,4,2,3}.

The idea is: 1) find the mid point; 2) reverse the second part; 3) merge two lists.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return
        # fast, slow pointer to find the mid point
        fast, slow = head, head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
        # cut in half
        secPart = slow.next
        slow.next = None
        # reverse the second part
        prev = None
        while secPart:
            cur = secPart
            secPart = secPart.next
            cur.next = prev
            prev = cur
        # merge two lists
        fstPart = head
        secPart = prev
        while fstPart:
            if secPart:
                tmp = fstPart.next
                fstPart.next = secPart
                tmp2 = secPart.next
                secPart.next = tmp
                secPart = tmp2
                fstPart = tmp
            else:
                break
```
