# Plus One Linked List

> Given a non-negative number represented as a singly linked list of digits, plus one to the number.

> The digits are stored such that the most significant digit is at the head of the list.

> Example:

> ```
Input:  1->2->3
Output: 1->2->4
```

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def plusOne(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # reverse list
        tail = None
        while head:
            head.next, head, tail = tail, head.next, head
        # plus one
        carry = 1
        while tail:  # now tail is the start of the list
            carry, tail.val = (carry + tail.val) / 10, (carry + tail.val) % 10
            if carry and not tail.next:
                tail.next = ListNode(0)
            # reverse back
            tail.next, tail, head = head, tail.next, tail
        return head
```
