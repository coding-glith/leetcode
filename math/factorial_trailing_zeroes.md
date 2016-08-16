# Factorial Trailing Zeroes

> Given an integer n, return the number of trailing zeroes in n!.

> Note: Your solution should be in logarithmic time complexity.

Check the explanations [here](http://www.purplemath.com/modules/factzero.htm). The idea is to find out how many 5*2 pairs are.

```Python
class Solution(object):
    def trailingZeroes(self, n):
        """
        :type n: int
        :rtype: int
        """
        res, count = 0, 1
        while n / (5 ** count):
            res += n / (5 ** count)
            count += 1
        return res
```
