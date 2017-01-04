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

# Valid Perfect Square

> Given a positive integer num, write a function which returns True if num is a perfect square else False.

> Note: Do not use any built-in library function such as sqrt.

> Example 1:

> ```
Input: 16
Returns: True
```

> Example 2:

> ```
Input: 14
Returns: False
```

```Python
class Solution(object):
    def isPerfectSquare(self, num):
        """
        :type num: int
        :rtype: bool
        """
        if num == 0:
            return True
        left, right = 1, num
        while left <= right:
            mid = left + (right - left) / 2
            if mid * mid == num:
                return True
            elif mid * mid > num:
                right = mid -1
            else:
                left = mid + 1
        return False 
```
