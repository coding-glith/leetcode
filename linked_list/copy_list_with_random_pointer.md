# Copy List with Random Pointer

> A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

> Return a deep copy of the list.

```Python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        if not head:
            return head
        # insert copy of nodes
        h = head
        while h:
            node = RandomListNode(h.label)
            node.random = h.random
            tmp = h.next
            h.next = node
            node.next = tmp
            h = tmp
        # adjust random pointer to correct node
        h = head.next
        while h:
            if h.random:
                h.random = h.random.next
            if not h.next:
                break
            h = h.next.next
        # disconnect original and copied list
        h = head
        dummy = RandomListNode(0)
        p = dummy
        while h:
            tmp = h.next
            p.next = tmp
            p = tmp
            tmp2 = tmp.next
            h.next = tmp.next
            h = tmp.next
        return dummy.next
```
