# Palindrome Linked List

> Given a singly linked list, determine if it is a palindrome.

> Follow up:

> Could you do it in O(n) time and O(1) space?

The idea is to find the middle node, then reverse the first part, and compare the two subList one by one, and revser the list back.

> ```
1->2->3->2->1 becomes:
1<-2--3->2->1
   p  h  t
1->2->3->3->2->1 becomes:
1<-2<-3--3->2->1
      p h/t
```

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
        prev, fast = None, head
        while fast and fast.next:
            fast = fast.next.next
            prev, prev.next, head = head, prev, head.next
        tail = head.next if fast else head   # deal with odd/even number cases
        # uptill now, the first half part is reversed
        # and rev is the head of the reversed list
        result = True
        while prev:
            if prev.val != tail.val: result = False
            prev, tail, head, head.next = prev.next, tail.next, prev, head   # need to move head to prev then assign head.next
        return result
```
