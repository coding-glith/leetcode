# Linked List Cycle

> Given a linked list, determine if it has a cycle in it.

> Follow up:

> Can you solve it without using extra space?

Define fast and slow pointer to check if has cycle, because if has cycle, fast and slow pointer will meet at some point.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if head == None or head.next == None:
            return False
        fast, slow = head, head
        while fast.next != None and fast.next.next != None:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True
        return False
```

# Linked List Cycle II

> Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

> Note: Do not modify the linked list.

> Follow up:

> Can you solve it without using extra space?

```Python

```
