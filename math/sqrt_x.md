# Sqrt(x)

> Implement int sqrt(int x).

> Compute and return the square root of x.

```Python
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x == 0:
            return 0
        left, right = 1, x
        while left <= right:
            mid = left + (right - left) / 2
            if mid > x / mid:
                right = mid - 1
            else:
                if mid + 1 > x / (mid + 1):
                    return mid
                left = mid + 1
```
