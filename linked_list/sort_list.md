# Sort List

> Sort a linked list in O(n log n) time using constant space complexity.

The idea of merge sort is to sort two list separately then merge them as one list. This is the divide and conquer method.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:  # should have checked head.next as well
            return head
        fast, slow = head, head
        # cut the list in half
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
        fast = slow.next
        slow.next = None
        # sort the two list separately
        p1 = self.sortList(head)
        p2 = self.sortList(fast)
        # merge two sorted list
        return self.merge(p1, p2)

    def merge(self, l1, l2):
        if not l1:
            return l2
        elif not l2:
            return l1
        elif not l1 and l2:
            return None
        dummy = ListNode(0)
        p = dummy
        while l1 and l2:
            if l1.val < l2.val:
                p.next = l1
                l1 = l1.next
            else:
                p.next = l2
                l2 = l2.next
            p = p.next
        if l1:
            p.next = l1
        elif l2:
            p.next = l2
        return dummy.next
```

# Insertion Sort List

> Sort a linked list using insertion sort.

For insertion sort, we check the node one by one. For node i+1, we need to check node 0:i and insert i+1 at correct location.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        dummy = ListNode(0)
        dummy.next = head
        cur = head
        while cur.next:
            if cur.next.val < cur.val:  # put smaller value ahead
                prev = dummy
                while prev.next.val < cur.next.val:
                    prev = prev.next
                # do insertion
                tmp = cur.next
                cur.next = tmp.next
                tmp.next = prev.next
                prev.next = tmp
            else:
                cur = cur.next
        return dummy.next
```
