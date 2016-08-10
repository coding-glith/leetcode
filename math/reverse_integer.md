# Reverse Integer

> Reverse digits of an integer.

> Example1: x = 123, return 321

> Example2: x = -123, return -321

```Python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x == 0:
            return x
        result = 0
        sign = 1 if x > 0 else -1
        x = abs(x)
        while x != 0:
            result = result * 10 + x % 10
            x = x / 10
        if result > 2**31+1:
            return 0
        return result * sign
```
