# Stack and Queue

> * [Simplify Path](simplify_path.md)

### Stack

Linkedlist implementation below. For array implementation, need to resize the array size.

```Python
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None
        
class LinkedListStack(object):
    def __init__(self):
        self.head = None
        
    def isEmpty(self):
        return self.head == None

    def push(self, val):
        # add to the head of linked list
        oldHead = self.head
        self.head = ListNode(val)
        self.head.next = oldHead

    def pop(self):
        oldHead = self.head
        self.head = self.head.next
        return oldHead.val
```

### Queue

Linkedlist implementation.

```Python
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None
        
class LinkedListStack(object):
    def __init__(self):
        self.head = None
        self.tail = None
        
    def isEmpty(self):
        return self.head == None

    def enqueue(self, val):
        # add to the tail of linked list
        oldTail = self.tail
        self.tail = ListNode(val)
        self.tail.next = None
        if self.isEmpty(): self.first = self.tail
        else: oldTail.next = self.tail

    def dequeue(self):
        oldHead = self.head
        self.head = self.head.next
        if self.isEmpty(): self.tail = None
        return oldHead.val
```
