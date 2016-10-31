# Remove Duplicates from Sorted List

> Given a sorted linked list, delete all duplicates such that each element appear only once.

> For example,

> Given 1->1->2, return 1->2.

> Given 1->1->2->3->3, return 1->2->3.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head: return None
        p = head
        while p.next:
            if p.val == p.next.val:
                p.next = p.next.next
            else:
                p = p.next
        return head
```

# Remove Duplicates from Sorted List II

> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

> For example,

> Given 1->2->3->3->4->4->5, return 1->2->5.

> Given 1->1->1->2->3, return 2->3.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next: return head
        dummy = ListNode(0)
        p = dummy
        while head and head.next:
            if head.val != head.next.val:
                p.next = ListNode(head.val)
                p = p.next
            else:
                while head.next and head.val == head.next.val:
                    head = head.next
            head = head.next
        if head: p.next = head
        return dummy.next
```

The idea is to create a dummy node before the head, and use that pointer as the previous unique value representer to help detect duplicate node.

```Python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        dummy = ListNode(0)
        dummy.next = head
        traverse = head
        prev = dummy
        while traverse and traverse.next:
            if traverse.val != traverse.next.val:
                prev = traverse
                traverse = traverse.next
            else: # if duplicate, find the next unique node
                while traverse and prev.next.val == traverse.val:
                    traverse = traverse.next
                prev.next = traverse
        return dummy.next
```
