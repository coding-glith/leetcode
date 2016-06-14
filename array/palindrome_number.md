# Palindrome Number

> Determine whether an integer is a palindrome. Do this without extra space.

```Python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        result, val = 0, x
        while val != 0:
            result = result * 10 + val % 10
            val /= 10
        return x == result
```
