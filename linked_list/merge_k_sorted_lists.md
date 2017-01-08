# Merge Two Sorted Lists

> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(0)
        p = dummy
        while l1 and l2:
            if l1.val < l2.val: p.next = ListNode(l1.val); l1 = l1.next
            else: p.next = ListNode(l2.val); l2 = l2.next
            p = p.next
        tmp = l1 if l1 else l2
        while tmp:
            p.next = ListNode(tmp.val)
            tmp, p = tmp.next, p.next
        return dummy.next
```

# Merge k Sorted Lists

> Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

The idea is to do "merge two lists" and slowly merge k lists into one.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if len(lists) == 0:
            return None
        while len(lists) > 1:
            nextLists = []
            # merge i and i+1
            for indx in xrange(0, len(lists)-1, 2):
                nextLists.append(self.mergeTwoLists(lists[indx], lists[indx+1]))
            # check for odd case
            if len(lists) % 2 == 1:
                nextLists.append(lists[len(lists)-1])
            lists = nextLists
        return lists[0]
        
    def mergeTwoLists(self, l1, l2):
        if not l1:
            return l2
        if not l2:
            return l1
        dummy = ListNode(0)
        result = dummy
        while l1 and l2:
            if l1.val <= l2.val:
                dummy.next = l1
                l1 = l1.next
            else:
                dummy.next = l2
                l2 = l2.next
            dummy = dummy.next
        if l1:
            dummy.next = l1
        if l2:
            dummy.next = l2
        return result.next
```
