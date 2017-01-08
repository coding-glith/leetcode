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
        dummy = ListNode(0)
        p, calculate = dummy, 0
        while l1 or l2:
            if l1: calculate += l1.val; l1 = l1.next
            if l2: calculate += l2.val; l2 = l2.next
            p.next = ListNode(calculate % 10)
            calculate /= 10
            p = p.next
        if calculate == 1:
            p.next = ListNode(calculate)
        return dummy.next
```

# Add Two Numbers II

> You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

> You may assume the two numbers do not contain any leading zero, except the number 0 itself.

> Follow up:

> What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

> Example:

> ```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

The idea is to use stack to store the value of two linked list. Then contruct the head of the sum linked list. 

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
        stack1, stack2 = [], []
        while l1:
            stack1.append(l1.val)
            l1 = l1.next
        while l2:
            stack2.append(l2.val)
            l2 = l2.next
        node = ListNode(0)
        calculate = 0
        while stack1 or stack2:
            if stack1: calculate += stack1.pop()
            if stack2: calculate += stack2.pop()
            node.val = calculate % 10
            newNode = ListNode(calculate / 10)
            newNode.next = node
            node = newNode
            calculate /= 10
        if node.val == 0 and node.next:
            return node.next
        return node
```
