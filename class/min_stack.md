# Min Stack

> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

> * push(x) -- Push element x onto stack.

> * pop() -- Removes the element on top of the stack.

> * top() -- Get the top element.

> * getMin() -- Retrieve the minimum element in the stack.

> Example:

> ```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

```Python
class MinStack(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.l = []
        self.minL = []
        
    def push(self, x):
        """
        :type x: int
        :rtype: void
        """
        self.l.append(x)
        if self.minL == []:
            self.minL.append(x)
        else:
            if x < self.minL[-1]:
                self.minL.append(x)
            else:
                self.minL.append(self.minL[-1])

    def pop(self):
        """
        :rtype: void
        """
        self.l.pop()
        self.minL.pop()

    def top(self):
        """
        :rtype: int
        """
        return self.l[-1]

    def getMin(self):
        """
        :rtype: int
        """
        return self.minL[-1]

# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
