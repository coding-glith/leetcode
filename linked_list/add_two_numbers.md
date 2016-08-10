# Add Two Numbers

> You are given two linked lists representing two non-negative numbers.

> The digits are stored in reverse order and each of their nodes contain a single digit.

> Add the two numbers and return it as a linked list.

> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

> Output: 7 -> 0 -> 8

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if not l1:
            return l2
        if not l2:
            return l1
        dummy = ListNode(0)
        p = dummy
        count = 0
        while l1 or l2:
            if not l1:
                sumVal = l2.val + count
            elif not l2:
                sumVal = l1.val + count
            else:
                sumVal = l1.val + l2.val + count
            p.next = ListNode(sumVal % 10)
            count = sumVal / 10
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
            p = p.next
        if count != 0:
            p.next = ListNode(count)
        return dummy.next   
```
