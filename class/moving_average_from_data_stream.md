# Moving Average from Data Stream

> Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

> For example,

> ```
MovingAverage m = new MovingAverage(3);
m.next(1) = 1
m.next(10) = (1 + 10) / 2
m.next(3) = (1 + 10 + 3) / 3
m.next(5) = (10 + 3 + 5) / 3
```

```Python
class MovingAverage(object):

    def __init__(self, size):
        """
        Initialize your data structure here.
        :type size: int
        """
        self.arr = []
        self.size = size
        

    def next(self, val):
        """
        :type val: int
        :rtype: float
        """
        if len(self.arr) < self.size:
            self.arr.append(val)
        else:
            for i in xrange(self.size-1):
                self.arr[i] = self.arr[i+1]
            self.arr[self.size-1] = val
        return sum(self.arr) / float(len(self.arr))
        


# Your MovingAverage object will be instantiated and called as such:
# obj = MovingAverage(size)
# param_1 = obj.next(val)
```
