# Sort Array Using Stack

```
original: [1, 5, 4, 3, 6, 7, 2, 8, 9]
stack:    [1, 5, 4, 3, 6, 7]
tmpStack: [9, 8, 2]
stack:    [1, 5, 4, 3, 6, 2]
tmpStack: [9, 8, 7]
stack:    [1, 5, 4, 3, 6]
tmpStack: [9, 8, 7, 2]
stack:    [1, 5, 4, 3, 2]
tmpStack: [9, 8, 7, 6]
and so on.
```

```Python
class Solution:
    def sortByStack(self, stack):
        tmpStack = []   # tmpStack should be in descending order
        while stack:
            cur = stack.pop()
            while tmpStack and cur > tmpStack[-1]:
                tmp = tmpStack.pop()
                stack.append(tmp)
            tmpStack.append(cur)
        while tmpStack:
            stack.append(tmpStack.pop())
```
