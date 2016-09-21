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

Based on previous question, we first check if there has cycle. The idea is that at first, slow move one node while fast move two nodes. When they fisrt met, reset fast pointer to "begin" and move one node at a time. When they met for the second time, the point is the "start" of the cycle. 

```
                  meet
                  n5 -> n6
                  |     |
n1 -> n2 -> n3 -> n4 <- n7
begin             start
```

Reason: "begin"->"start" = a, "start"->"meet" = b, "meet"->"start" = c.

for first meet: fast = a+b+c+b; slow = a+b

fast = 2\*slow: (a+b+c+b) = 2\*(a+b); so a = c.

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

# Find the Duplicate Number

> Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

> Note:

> * You must not modify the array (assume the array is read only).

> * You must use only constant, O(1) extra space.

> * Your runtime complexity should be less than O(n2).

> * There is only one duplicate number in the array, but it could be repeated more than once.

The key idea is to play with the index and value to form a circle.

say,

```
index: 0,1,2,3,4,5
value: 2,5,4,1,3,3
circle: 2->4->3->5-
              ^   |
              |<--|
```

```Python
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        slow, fast = nums[0], nums[nums[0]]
        while slow != fast:
            slow = nums[slow]
            fast = nums[nums[fast]]
        fast = 0
        while slow != fast:
            slow = nums[slow]
            fast = nums[fast]
        return slow
```
