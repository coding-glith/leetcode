# Happy Number

> Write an algorithm to determine if a number is "happy".

> A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

> Example: 19 is a happy number

> ```
1**2 + 9**2 = 82
8**2 + 2**2 = 68
6**2 + 8**2 = 100
1**2 + 0**2 + 0**2 = 1
```

This solution uses slow and fast pointers. "slow" calculates square sum once while "fast" calculates sqaure sum twice. If is happy number, they will meet at 1, otherwise, this sqaure sum will become a circle, and they will finally meet at some point other than 1.

```Python
class Solution(object):
    def isHappy(self, n):
        """
        :type n: int
        :rtype: bool
        """
        slow = self.digitSqaureSum(n)
        fast = self.digitSqaureSum(n)
        fast = self.digitSqaureSum(fast)
        while slow != fast:
            slow = self.digitSqaureSum(slow)
            fast = self.digitSqaureSum(fast)
            fast = self.digitSqaureSum(fast)
        if slow == 1:
            return True
        else:
            return False

    def digitSqaureSum(self, n):
        squareSum = 0
        while n:
            tmp = n % 10
            squareSum += tmp * tmp
            n /= 10
        return squareSum
```
