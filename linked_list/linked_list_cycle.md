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

> ```
                  meet
                  n5 -> n6
                  |     |
n1 -> n2 -> n3 -> n4 <- n7
begin             start
```

Based on previous question, we first check if there has cycle. The idea is that at first, slow move one node while fast move two nodes. When they fisrt met, reset fast pointer to "begin" and move one node at a time. When they met for the second time, the point is the "start" of the cycle. 

Reason: "begin"->"start" = a, "start"->"meet" = b, "meet"->"start" = c.

for first meet: fast = a+b+c+b; slow = a+b

fast = 2*slow: (a+b+c+b) = 2*(a+b); so a = c.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None or head.next == None:
            return None
        fast, slow = head, head
        while fast.next != None and fast.next.next != None:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                fast = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        return None
```
