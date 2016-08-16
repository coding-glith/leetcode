# Palindrome Linked List

> Given a singly linked list, determine if it is a palindrome.

> Follow up:

> Could you do it in O(n) time and O(1) space?

The idea is to find the middle node, then reverse the first part, and compare the two subList one by one.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def isPalindrome(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        rev, fast = None, head
        while fast and fast.next:
            fast = fast.next.next
            rev, rev.next, head = head, rev, head.next
        tail = head.next if fast else head
        isPali = True
        while rev:
            isPali = (isPali and rev.val == tail.val)
            head, head.next, rev = rev, head, rev.next
            tail = tail.next
        return isPali
```
