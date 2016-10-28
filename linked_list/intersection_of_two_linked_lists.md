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

This solution is based on running a+b and b+a to find the intersection.

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
        a, b = headA, headB
        while a != b:
            a = a.next if a else headB
            b = b.next if b else headA
        return a
```

This solution is based on "Linked List Cycle" to find the start point of a cycle.

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

This solution is find the length of both lists and after go through the more nodes in the longer list, search it one by one until find an intersection. Didn't understand why all these three solution gets memory limit exceeded error. The previous two solution passed the first time I submit it.

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
        def listLength(head):
            res = 0
            while head:
                res += 1
                head = head.next
            return res
        a, alen, b, blen = headA, listLength(headA), headB, listLength(headB)
        if alen > blen:
            for i in xrange(alen-blen):
                a = a.next
        if blen > alen:
            for i in xrange(blen-alen):
                b = b.next
        while a != b:
            a, b = a.next, b.next
        return a
```
