# Intersection of Two Linked Lists

> Write a program to find the node at which the intersection of two singly linked lists begins.

> For example, the following two linked lists:

> ```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

> begin to intersect at node c1.

> Notes:

> * If the two linked lists have no intersection at all, return null.

> * The linked lists must retain their original structure after the function returns.

> * You may assume there are no cycles anywhere in the entire linked structure.

> * Your code should preferably run in O(n) time and use only O(1) memory.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        if not headA or not headB:
            return None
        # traverse A
        traverseA = headA
        while traverseA.next:
            traverseA = traverseA.next
        # connect the tail of A with head of B
        traverseA.next = headB
        tailA = traverseA  # copy it for later recovery
        traverseA = headA
        # use fast/slow to check if there's cycle
        headB = headA
        while headB.next and headB.next.next:
            headA = headA.next
            headB = headB.next.next
            if headA == headB:
                break
        # if no cycle, break connection and return None
        if not headA.next or not headB.next or not headB.next.next:
            tailA.next = None
            return None
        # if there's cycle, get the start point of the cycle
        headA = traverseA
        while headA != headB:
            headA = headA.next
            headB = headB.next
        # break the connection
        tailA.next = None
        return headA
```
