# Divide Two Integers

> Divide two integers without using multiplication, division and mod operator.

> If it is overflow, return MAX_INT.

Since we cannot use mutiplication, division and mod, we can consider using addition and subtraction.

If we do subtraction directly, then it's time consuming. So in the second loop, we are doubling the divisor.

```Python
class Solution(object):
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        if divisor == 0: return -1
        flag = 1 if (dividend >= 0 and divisor >= 0) or (dividend < 0 and divisor < 0) else -1
        dividend, divisor = abs(dividend), abs(divisor)
        res, count = 0, 0
        while dividend >= divisor:
            count = 1
            tmp = divisor
            while dividend >= tmp:
                dividend -= tmp
                res += count
                count += count
                tmp += tmp
        if res > 2147483647: return 2147483647 if flag == 1 else -2147483648
        return res * flag
```
